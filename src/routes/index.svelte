<svelte:head>
  <title>Bad Decision Maker</title>
</svelte:head>

<section>
  <div class="paper-container">
    <a href="/create" rel=prefetch>
      <Paper color="primary" class="paper">
        <Title>Make bad decisions faster</Title>
        <Content>Never before has it been this easy to commit to terrible ideas.</Content>
      </Paper>
    </a>
  </div>

  <Fab/>
</section>

<script>
  import Paper, {Title, Subtitle, Content} from '@smui/paper';
  import Fab from '../components/fab.svelte';
</script>

<style>
  a {
    text-decoration: none;
  }

  .paper-container {
    margin-left: auto;
    margin-right: auto;
    max-width: 600px;
  }

  .paper-container {
    cursor: pointer;
  }
</style>
