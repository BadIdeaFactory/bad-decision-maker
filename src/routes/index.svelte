<svelte:head>
  <title>Bad Decision Maker</title>
</svelte:head>

<section>
  <div class="paper-container">
    <Paper color="primary" class="paper" on:click={() => sapper.goto('/create')}>
      <Title>Make bad decisions faster</Title>
      <Content>Never before has it been this easy to commit to terrible ideas.</Content>
    </Paper>
  </div>
</section>

<script>
  import * as sapper from '@sapper/app';

  import Paper, {Title, Subtitle, Content} from '@smui/paper';
  import A from '@smui/common/A.svelte';
</script>

<style>
  .paper-container {
    margin-left: auto;
    margin-right: auto;
    max-width: 600px;
  }

  .paper-container {
    cursor: pointer;
  }
</style>
