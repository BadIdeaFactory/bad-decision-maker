<svelte:head>
  <title>Bad Decision Maker</title>
</svelte:head>

<section>
  <div class="create-container">
    <h2 style="margin-bottom: 0;padding-bottom: 0">Create</h2>

    <div>
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
        <div class="field-container">
          <Textfield style="flex-grow: 1;" variant="outlined" bind:value={option1} label="Option 1" />
        </div>
        <div class="field-container">
          <Textfield style="flex-grow: 1;" variant="outlined" bind:value={option1} label="Option 2" />
        </div>
        <div class="field-container">
          <a href="/vote" rel=prefetch>
              <Button variant="raised"><Label>Create</Label></Button>
          </a>
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
  let creator = '';
  let description = '';
  let option1 = '';
  let option2 = '';
</script>

<style>
  a {
    text-decoration: none;
  }
  
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
