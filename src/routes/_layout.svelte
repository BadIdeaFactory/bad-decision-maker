<svelte:window />
  <TopAppBar variant="standard" class="top-app-bar">
    <Row>
      <Section>
        <Title component={A} href="/" class="mdc-theme--primary">
          Bad Decision Maker
        </Title>
      </Section>
    </Row>
  </TopAppBar>
  <main class="main-content">
    <slot></slot>

    <div class="fab">
      <a href="/create" rel=prefetch>
        <Fab><Icon class="material-icons">add</Icon></Fab>
      </a>
    </div>
  </main>

<script>
  import './_app.scss';

  import TopAppBar, {Row, Section, Title} from '@smui/top-app-bar';
  import Fab, {Label, Icon} from '@smui/fab';
  import A from '@smui/common/A.svelte';
</script>

<style>
.fab {
  position: absolute;
  bottom: 20px;
  right: 20px;
}

.main-content {
  padding: 80px;
}
</style>
