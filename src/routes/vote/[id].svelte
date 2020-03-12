<svelte:head>
  <title>{poll.title} - Bad Decision Maker</title>
</svelte:head>

<section>
  <div>
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

    {#if options}
      {#each options as option}
        <div class="field-container">
          <Button class="bigger" variant="outlined" style="flex-grow: 1;" on:click="{() => vote(option)}" disabled={option.voted}><Label>{ option.voted ? '✓' : ''} {option.name}</Label></Button>
        </div>
        {#if option.votes.length > 0}
        <div class="votes-container">
          <p>
            {capFirst(apnumber(option.votes.length))} vote{option.votes.length > 1 ? 's' : ''} from {option.votes.filter(vote => vote.creator).map(vote => vote.creator).join(', ')}{option.votes.filter(vote => vote.creator).length > 0 && option.votes.filter(vote => !vote.creator).length > 0 ? ' and ' : ''}{option.votes.filter(vote => !vote.creator).length > 0 ? `${apnumber(option.votes.filter(vote => !vote.creator).length)} anonymous voters` : ''}.
          </p>
        </div>
        {/if}
      {/each}
    {/if}
  </div>

  <Fab/>
</section>

<script context="module">
  export async function preload(page, session) {
    const { id } = page.params;

    const res = await this.fetch(`https://api.baddecisions.app/polls/${id}`);
    const poll = await res.json();

    return { poll };
  }
</script>

<script>
  import { onMount, onDestroy } from 'svelte';
  import Fab from '../../components/fab.svelte';
  import Button, { Label } from '@smui/button';
  import Textfield, {Input, Textarea} from '@smui/textfield';
  import { apnumber } from 'journalize';
  import marked from 'marked';
  import insane from 'insane';

  import {
    userInfo,
  } from '@dopry/svelte-auth0';

  let creator = '';
  let error = '';
  let timer = null;
  
  const unsubscribe = userInfo.subscribe(value => {
    creator = value && value.name ? value.name : '';
  });

  onDestroy(unsubscribe);

  export let poll;

  const votes = poll.votes.sort((a,b) => a.createdAt-b.createdAt);

  let options = poll.options.map(option => ({
    name: option,
    votes: votes.filter(vote => vote.option === option),
    voted: false
  }));

  function capFirst(string) {
      return string.charAt(0).toUpperCase() + string.slice(1);
  }

  async function refreshPoll () {
    const res = await fetch(`https://api.baddecisions.app/polls/${poll.id}`);
    const updatedPoll = await res.json();

    const votes = updatedPoll.votes.sort((a,b) => a.createdAt-b.createdAt);

    options.forEach(option => {
      option.votes = votes.filter(vote => vote.option === option.name)
    });

    options = options;
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
  }

  onMount(() => {
    refreshPoll();

    timer = setInterval(refreshPoll,10000);
  });

  onDestroy(() => {
    if (timer) {
      clearInterval(timer);
    }
  });
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
