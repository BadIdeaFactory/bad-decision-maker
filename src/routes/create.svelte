<svelte:head>
  <title>Bad Decision Maker</title>
</svelte:head>

<section>
  <h1>Create</h1>

  <div>
    <div class="margins">
      <div>
        <Textfield bind:value={title} label="Title" />
        <!-- input$aria-controls="helper-text-title" input$aria-describedby="helper-text-title"
        <HelperText id="helper-text-title">Title</HelperText>
        -->
      </div>
      <div>
        <Textfield bind:value={description} label="Description" />
      </div>
      <div>
        <Textfield bind:value={option1} label="Option 1" />
      </div>
      <div>
        <Textfield bind:value={option1} label="Option 2" />
      </div>
  </div>
</section>

<script>
  import Textfield, {Input, Textarea} from '@smui/textfield';
  import Icon from '@smui/textfield/icon/index';
  import HelperText from '@smui/textfield/helper-text/index';

  let title = '';
  let description = '';
  let option1 = '';
  let option2 = '';
</script>

<style>
  .margins {
    margin: 18px 0 24px;
  }
</style>
