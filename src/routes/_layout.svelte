<TopAppBar variant="standard" class="top-app-bar">
  <Row style="padding-left: 20px;padding-right: 20px">
    <Section style="max-width: 700px;margin-right: auto;margin-left: auto;padding: 0">
      <Title component={A} href="/" rel=prefetch class="mdc-theme--primary" style="padding-left: 0">
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
  padding-top: 35px;
}
</style>
