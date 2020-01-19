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
      <Textfield style="flex-grow: 1;" variant="outlined" bind:value={name} label="Your name" />
    </div>

    {#if poll.options}
      {#each poll.options as option}
        <div class="field-container">
          <Button variant="outlined" style="flex-grow: 1;"><Label>{option}</Label></Button>
          <!--  on:click={() => option1++}  ({option1})-->
        </div>
      {/each}
    {/if}
  </div>

  <Fab/>
</section>

<script context="module">
  export async function preload(page, session) {
    const { id } = page.params;

    const res = await this.fetch(`https://6ykntbtg61.execute-api.us-east-1.amazonaws.com/dev/polls/${id}`);
    const poll = await res.json();

    return { poll };
  }
</script>

<script>
  import Fab from '../../components/fab.svelte';
  import Button, { Label } from '@smui/button';
  import Textfield, {Input, Textarea} from '@smui/textfield';

  let name = '';

  export let poll;
</script>

<style>
  .poll-container {
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
