<Auth0Context
  domain="zubakskees-dev.auth0.com"
  client_id="W50D4SXZKJIBh2ekamhD6UwCcfe0V9ap"
  callback_url={window.location.origin}
  logout_url={window.location.origin}
>
  <div class="app-container">
    <TopAppBar variant="standard" class="top-app-bar">
      <Row style="max-width: 850px;">
        <Section style="padding: 0">
          <Title component={A} href="/" rel=prefetch class="mdc-theme--primary">
            Bad Decision Maker
          </Title>
        </Section>
        <Section align="end" toolbar>
          <IconButton on:click='{() => !$isAuthenticated ? login(false) : logout() }'>
            <Icon >
            {#if !$userInfo || !$userInfo.picture}
              <svg style="width:24px;height:24px" viewBox="0 0 24 24">
                <path fill="#000000" d="{mdiAccountCircleOutline}" />
              </svg>
            {:else}
              <img alt="user picture" style="width:24px;height:24px;border-radius: 50%;" src="{$userInfo.picture}" />
            {/if}
            </Icon>
          </IconButton>
        </Section>
      </Row>
    </TopAppBar>
    <main class="main-content">
      <slot></slot>
    </main>
  </div>
</Auth0Context>

<script>
  import './_app.scss';

  import TopAppBar, {Row, Section, Title} from '@smui/top-app-bar';
  import A from '@smui/common/A.svelte';
  import IconButton from '@smui/icon-button';
  import {Icon} from '@smui/common';

  import {
    Auth0Context,
    authError,
    authToken,
    isAuthenticated,
    isLoading,
    login,
    logout,
    userInfo,
  } from '@dopry/svelte-auth0';

  import {mdiAccountCircleOutline} from '@mdi/js';

  // https://github.com/BadIdeaFactory/random-bg-color/blob/master/src/index.js#L22
  const bifColors = [
    '#b3115a',
    '#af1781',
    '#883a8e',
    '#8f0863',
    '#54358c',
    '#625198',
    '#312783',
    '#24378d',
    '#224c9c',
    '#1d71b8',
    '#009c9b',
    '#31a936',
    '#9db41f',
    '#f39200',
    '#e94e1b',
    '#e6332a',
    '#e30613',
    '#be1622'
  ];

  const bifSecondaryColors = bifColors.concat(['#ffda00','#fcea10']);

  document
    .documentElement
    .style
    .setProperty('--mdc-theme-primary',
      bifColors[Math.floor(Math.random() * bifColors.length)]);

  document
    .documentElement
    .style
    .setProperty('--mdc-theme-secondary',
      bifColors[Math.floor(Math.random() * bifSecondaryColors.length)]);


</script>

<style>
.main-content {
  padding-top: 35px;
}
.app-container {
  max-width: 850px;
  margin-left: auto;
  margin-right: auto;
}
</style>
