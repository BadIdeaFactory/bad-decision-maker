<svelte:head>
  <title>{poll ? `${poll.title} -` : '' } Bad Decision Maker</title>
</svelte:head>

<section>
  <div>
    {#if poll}
      <h2 style="margin-bottom: 0;padding-bottom: 0">{poll.title}</h2>

      {#if poll.creator}
        <h3 class="mdc-typography--subtitle2" style="margin: 0 0; opacity:0.8;font-size: 15px">Created by {poll.creator} <!-- yesterday --></h3>
      {/if}

      {#if poll.description}
        <div class="markdown-body"><p>{@html insane(marked(poll.description,{ gfm:true }))}</p></div>
      {/if}

      {#if error}
        <div class="field-container">
          <span style="color: red">{error}</span>
        </div>
      {/if}

      <div class="field-container">
        <Textfield style="flex-grow: 1;" variant="outlined" bind:value={creator} label="Your name" />
      </div>

      <Dialog bind:this={confirmDialog} aria-labelledby="confirm-title" aria-describedby="confirm-content">
        <!-- Title cannot contain leading whitespace due to mdc-typography-baseline-top() -->
        <Title id="confirm-title">Vote anonymously?</Title>
        <Content id="confirm-content">
          You haven't entered a name. Count vote anonymously?
        </Content>
        <Actions>
          <Button on:click={() => selectedOption = null}>
            <Label>No</Label>
          </Button>
          <Button on:click={() => vote(selectedOption)}>
            <Label>Yes</Label>
          </Button>
        </Actions>
      </Dialog>

      {#if options}
        {#each options as option}
          <div class="field-container">
            <Button class="bigger" variant="outlined" style="flex-grow: 1;" on:click="{() => creator ? vote(option) : confirmVote(option)}" disabled={option.voted}><Label>{ option.voted ? '✓' : ''} {option.name}</Label></Button>
          </div>
          {#if option.votes.length > 0}
          <div class="votes-container">
            <p>
              <span style="padding-left: 8px">{capFirst(apnumber(option.votes.length))} vote{option.votes.length > 1 ? 's' : ''} from:</span>

              <Set chips={option.votes.filter(vote => vote.creator).map(vote => vote.creator).concat(option.votes.filter(vote => !vote.creator).length > 0 ? [`${apnumber(option.votes.filter(vote => !vote.creator).length)} anonymous voters`] : [])} let:chip style="padding: 0">
                <Chip><Text>{chip}</Text></Chip>
              </Set>
            </p>
          </div>
          {/if}
        {/each}
      {/if}
    {/if}
  </div>

  <Fab/>
</section>

<script>
  import { stores } from '@sapper/app';
  import Dialog, {Title, Content, Actions, InitialFocus} from '@smui/dialog';
  import { onMount, onDestroy } from 'svelte';
  import Fab from '../../components/fab.svelte';
  import Button, { Label } from '@smui/button';
  import Textfield, {Input, Textarea} from '@smui/textfield';
  import List, {Item, Graphic, Text} from '@smui/list';
  import Chip, {Set} from '@smui/chips';
  import { apnumber } from 'journalize';
  import marked from 'marked';
  import insane from 'insane';

  import {
    userInfo,
  } from '@dopry/svelte-auth0';

  const { page } = stores();
  const { id } = $page.params;
  let poll = null;
  let options = [];
  let creator = '';
  let error = '';
  let timer = null;
  let confirmDialog;
  let selectedOption = null;
  
  const unsubscribe = userInfo.subscribe(value => {
    creator = value && value.name ? value.name : '';
  });

  onDestroy(unsubscribe);

  function capFirst(string) {
      return string.charAt(0).toUpperCase() + string.slice(1);
  }

  async function refreshPoll () {
    const res = await fetch(`https://api.baddecisions.app/polls/${id}`);
    poll = await res.json();

    const votes = poll.votes.sort((a,b) => a.createdAt-b.createdAt);

    options = poll.options.map(option => ({
      name: option,
      votes: votes.filter(vote => vote.option === option),
      voted: false
    }));

    options = options;
  }

  function confirmVote(option) {
    selectedOption = option;

    confirmDialog.open();
  }

  async function vote(option) {
    const body = {
      id: poll.id,
      option: option.name,
      creator
    };

    try {
      option.votes.push(body);
      option.voted = true;
      options = options;
      error = null;

      const res = await fetch('https://api.baddecisions.app/polls/vote', {
        method: 'post',
        body: JSON.stringify(body)
      });

      if (res.status !== 200) {
        throw new Error(((await res.json()).message));
      }

      const vote = await res.json();
    }
    catch (e) {
      option.votes.pop();
      option.voted = false;
      options = options;

      error = 'Failed to vote.';
    }

    selectedOption = null;
  }

  onMount(() => {
    refreshPoll();

    // timer = setInterval(refreshPoll, 5000);
  });
/*
  onDestroy(() => {
    if (timer) {
      clearInterval(timer);
    }
  });
*/
</script>

<style>
  .votes-container {
    padding-bottom: 10px;
  }

  .field-container {
    display: flex;
    padding-top: 10px;
  }
</style>
