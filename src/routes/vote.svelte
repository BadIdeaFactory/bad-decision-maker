<svelte:head>
  <title>Bad Decision Maker</title>
</svelte:head>

<section>
  <div class="poll-container">
    <h1>Poll name</h1>

    <p>Poll description goes here</p>

    <div class="field-container">
      <Textfield fullwidth bind:value={name} label="Name" />
    </div>

    <div class="field-container">
      <Button variant="outlined" style="flex-grow: 1;"><Label>Option 1</Label></Button>
    </div>
    <div class="field-container">
      <Button variant="outlined" style="flex-grow: 1;"><Label>Option 2</Label></Button>
    </div>
    <div class="field-container">
      <Button variant="outlined" style="flex-grow: 1;"><Label>Option 3</Label></Button>
    </div>
  </div>

  <Fab/>
</section>

<script>
  import Fab from '../components/fab.svelte';
  import Button, { Label } from '@smui/button';
  import Textfield, {Input, Textarea} from '@smui/textfield';

  let name = '';
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
