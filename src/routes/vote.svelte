<svelte:head>
  <title>Bad Decision Maker</title>
</svelte:head>

<section>
  <div class="poll-container">
    <h2 style="margin-bottom: 0;padding-bottom: 0">Poll title</h2>

    <h3 class="mdc-typography--subtitle2" style="margin: 0 0; color: #888;font-size: 15px">Created by slifty yesterday</h3>

    <p>Poll description goes here</p>

    <div class="field-container">
      <Textfield style="flex-grow: 1;" variant="outlined" bind:value={name} label="Your name" />
    </div>

    <div class="field-container">
      <Button variant="outlined" style="flex-grow: 1;" on:click={() => option1++}><Label>Option 1 ({option1})</Label></Button>
    </div>
    <div class="field-container">
      <Button variant="outlined" style="flex-grow: 1;" on:click={() => option2++}><Label>Option 2 ({option2})</Label></Button>
    </div>
    <div class="field-container">
      <Button variant="outlined" style="flex-grow: 1;" on:click={() => option3++}><Label>Option 3 ({option3})</Label></Button>
    </div>
  </div>

  <Fab/>
</section>

<script>
  import Fab from '../components/fab.svelte';
  import Button, { Label } from '@smui/button';
  import Textfield, {Input, Textarea} from '@smui/textfield';

  let name = '';
  let option1 = 0;
  let option2 = 0;
  let option3 = 0;
</script>

<style>
  .poll-container {
    margin-left: auto;
    margin-right: auto;
    max-width: 600px;
  }

  .field-container {
    display: flex;
    padding-top: 10px;
    padding-bottom: 10px;
  }
</style>
