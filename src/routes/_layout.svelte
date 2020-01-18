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
  </main>

<script>
  import './_app.scss';

  import TopAppBar, {Row, Section, Title} from '@smui/top-app-bar';
  import A from '@smui/common/A.svelte';
</script>

<style>
.main-content {
  padding-top: 60px;
}
</style>
