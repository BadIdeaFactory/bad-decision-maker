<svelte:head>
  <title>Bad Decision Maker</title>
</svelte:head>

<section>
  <div class="create-container">
    <h1>Create</h1>

    <div>
        <div class="field-container">
          <Textfield fullwidth bind:value={title} label="Title" id="title" />
          <!-- bind:this={titleEl} -->
          <!-- input$aria-controls="helper-text-title" input$aria-describedby="helper-text-title"
          <HelperText id="helper-text-title">Title</HelperText>
          -->
        </div>
        <div class="field-container">
          <Textfield fullwidth textarea bind:value={description} label="Description" />
        </div>
        <div class="field-container">
          <Textfield fullwidth bind:value={option1} label="Option 1" />
        </div>
        <div class="field-container">
          <Textfield fullwidth bind:value={option1} label="Option 2" />
        </div>
        <div class="field-container">
          <Button variant="raised"><Label>Create</Label></Button>
        </div>
    </div>
  </div>
</section>

<script>
  import {onMount} from 'svelte';
  import Textfield, {Input, Textarea} from '@smui/textfield';
  import Icon from '@smui/textfield/icon/index';
  import HelperText from '@smui/textfield/helper-text/index';
  import Button, { Label } from '@smui/button';

  let title = '';
  let description = '';
  let option1 = '';
  let option2 = '';

  /*
  let titleEl;

  onMount(() => {
    setTimeout(() => {
      titleEl.focus();
    },500);
  })*/
</script>

<style>
  .create-container {
    margin-left: auto;
    margin-right: auto;
    max-width: 600px;
  }

  .field-container {
    padding-top: 10px;
    padding-bottom: 10px;
  }
</style>
