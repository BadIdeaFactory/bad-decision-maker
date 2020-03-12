<svelte:head>
  <title>Bad Decision Maker</title>
</svelte:head>

<section>
  <div class="create-container">
    <h2 style="margin-bottom: 0;padding-bottom: 0">Create</h2>

    <div>
        <form on:submit|preventDefault={() => {}}>
          {#if error}
            <div class="field-container">
              <span style="color: red">{error}</span>
            </div>
          {/if}
          <div class="field-container">
            <Textfield style="flex-grow: 1;" variant="outlined" bind:value={title} label="Title" id="title" />
          </div>
          <div class="field-container">
            <Textfield style="flex-grow: 1;" variant="outlined" bind:value={creator} label="Your name" />
          </div>
          <div class="field-container">
            <Textfield style="flex: 0 0 100%;" variant="outlined" textarea bind:value={description} label="Description" id="input-description" aria-controls="helper-text-description" aria-describedby="helper-text-description" />
            <HelperText style="flex: 0 0 100%;" id="helper-text-description"><a href="https://guides.github.com/features/mastering-markdown/">Markdown formatting supported</a></HelperText>
          </div>
          {#each options as option, i}
          <div class="field-container">
            <EmojiSelector on:emoji={(event) => {onEmoji(event,i)}} />
            <Textfield style="flex-grow: 1;" variant="outlined" on:input={addOptions} bind:value={option} label="Option {i+1}" />
          </div>
          {/each}

          <div class="field-container">
                <Button variant="raised" type="submit" on:click={createPoll}><Label>Create</Label></Button>
          </div>

        </form>
    </div>
  </div>
</section>

<script>
  import { onDestroy } from 'svelte';
  import { goto } from '@sapper/app'
  import Textfield, {Input, Textarea} from '@smui/textfield';
  import Icon from '@smui/textfield/icon/index';
  import HelperText from '@smui/textfield/helper-text/index';
  import Button, { Label } from '@smui/button';
  import EmojiSelector from 'svelte-emoji-selector';

  import {
    userInfo,
  } from '@dopry/svelte-auth0';

  let title = '';
  let creator = '';
  let description = '';
  let options = ['',''];
  let error = null;

  const unsubscribe = userInfo.subscribe(value => {
    creator = value && value.name ? value.name : '';
  });

  onDestroy(unsubscribe);

  function onEmoji(event,i) {
    options[i] = event.detail + ' ' + options[i];
    addOptions();
  }

  function addOptions() {
    if (options[options.length-1] !== '') {
      options.push('');
    }
  }

  async function createPoll() {
    const body = {
      title,
      creator,
      description,
      options: options.filter(option => option !== '')
    };

    try {
      const res = await fetch('https://api.baddecisions.app/polls', {
        method: 'post',
        body: JSON.stringify(body)
      });

      if (res.status !== 200) {
        throw new Error(((await res.json()).message));
      }

      const poll = await res.json();

      goto(`/vote/${poll.id}`);

    }
    catch (e) {
      error = e.message;
    }
  }
</script>

<style>
  .field-container {
    flex-wrap: wrap;
    display: flex;
    padding-top: 10px;
    padding-bottom: 10px;
  }
</style>
