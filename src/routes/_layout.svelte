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
      <Fab on:click={() => sapper.goto('/create')}><Icon class="material-icons">add</Icon></Fab>
    </div>
  </main>

<script>
  import * as sapper from '@sapper/app';

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
