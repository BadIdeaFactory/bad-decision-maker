<svelte:head>
  <title>{poll.title} - Bad Decision Maker</title>
</svelte:head>

<section>
  <div class="poll-container">
    <h2 style="margin-bottom: 0;padding-bottom: 0">{poll.title}</h2>

    {#if poll.creator}
      <h3 class="mdc-typography--subtitle2" style="margin: 0 0; color: #888;font-size: 15px">Created by {poll.creator} <!-- yesterday --></h3>
    {/if}

    {#if poll.description}
      <p>{poll.description}</p>
    {/if}

    <div class="field-container">
      <Textfield style="flex-grow: 1;" variant="outlined" bind:value={creator} label="Your name" />
    </div>

    {#if poll.options}
      {#each poll.options as option}
        <div class="field-container">
          <Button variant="outlined" style="flex-grow: 1;" on:click="{() => vote(option)}"><Label>{option}</Label></Button>
        </div>
        {#if votes.filter(vote => vote.option === option).length > 0}
        <div class="votes-container">
          <p>
            {votes.filter(vote => vote.option === option).length} votes:
            {votes.filter(vote => vote.option === option).map(vote => vote.creator ? vote.creator : 'anonymous').join(', ')}
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

    const res = await this.fetch(`https://xuyhy09bx7.execute-api.us-east-1.amazonaws.com/dev/polls/${id}`);
    const poll = await res.json();

    return { poll };
  }
</script>

<script>
  import { onMount, onDestroy } from 'svelte';
  import Fab from '../../components/fab.svelte';
  import Button, { Label } from '@smui/button';
  import Textfield, {Input, Textarea} from '@smui/textfield';

  let creator = '';
  let error = '';
  let votes = [];
  let timer = null;

  export let poll;

  onMount(() => {
    votes = poll.votes.slice();

    timer = setInterval(async () => {
      const res = await fetch(`https://xuyhy09bx7.execute-api.us-east-1.amazonaws.com/dev/polls/${poll.id}`);
      const updatedPoll = await res.json();

      votes = updatedPoll.votes;
      poll.options = poll.options;
    },10000);
  });

  onDestroy(() => {
    if (timer) {
      clearInterval(timer);
    }
  });

  async function vote(option) {
    const body = {
      id: poll.id,
      option,
      creator
    };

    try {
      const res = await fetch('https://xuyhy09bx7.execute-api.us-east-1.amazonaws.com/dev/polls/vote', {
        method: 'post',
        body: JSON.stringify(body)
      });

      if (res.status !== 200) {
        throw new Error(((await res.json()).message));
      }

      const vote = await res.json();

      votes.push(vote);
      poll.options = poll.options;
    }
    catch (e) {
      error = e.message;
    }
  }
</script>

<style>
  .poll-container {
    margin-left: auto;
    margin-right: auto;
    max-width: 700px;
  }

  .votes-container {
    padding-bottom: 10px;
  }

  .field-container {
    display: flex;
    padding-top: 10px;
  }
</style>
