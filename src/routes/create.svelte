<svelte:head>
  <title>Bad Decision Maker</title>
</svelte:head>

<section>
  <div class="create-container">
    <h2 style="margin-bottom: 0;padding-bottom: 0">Create</h2>

    <div>
        <form on:submit|preventDefault={createPoll}>
          {#if error}
            <div class="field-container">
              <span style="color: red">{error}</span>
            </div>
          {/if}
          <div class="field-container">
            <Textfield style="flex-grow: 1;" variant="outlined" bind:value={creator} label="Your name" />
          </div>
          <div class="field-container">
            <Textfield style="flex-grow: 1;" variant="outlined" bind:value={title} label="Title" id="title" />
            <!-- bind:this={titleEl} -->
            <!-- input$aria-controls="helper-text-title" input$aria-describedby="helper-text-title"
            <HelperText id="helper-text-title">Title</HelperText>
            -->
          </div>
          <div class="field-container">
            <Textfield style="flex-grow: 1;" variant="outlined" textarea bind:value={description} label="Description" />
          </div>
          {#each options as option, i}
          <div class="field-container">
            <Textfield style="flex-grow: 1;" variant="outlined" on:input={addOptions} bind:value={option} label="Option {i+1}" />
          </div>
          {/each}

          <div class="field-container">
                <Button variant="raised" type="submit"><Label>Create</Label></Button>
          </div>

        </form>
    </div>
  </div>
</section>

<script>
  import { goto } from '@sapper/app'
  import Textfield, {Input, Textarea} from '@smui/textfield';
  import Icon from '@smui/textfield/icon/index';
  import HelperText from '@smui/textfield/helper-text/index';
  import Button, { Label } from '@smui/button';

  let title = '';
  let creator = '';
  let description = '';
  let options = ['',''];
  let error = null;

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
      const res = await fetch('https://xuyhy09bx7.execute-api.us-east-1.amazonaws.com/dev/polls', {
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
  .create-container {
    margin-left: auto;
    margin-right: auto;
    max-width: 700px;
  }

  .field-container {
    display: flex;
    padding-top: 10px;
    padding-bottom: 10px;
  }
</style>
