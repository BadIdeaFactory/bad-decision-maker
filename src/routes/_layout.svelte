<Auth0Context
  domain="zubakskees-dev.auth0.com"
  client_id="W50D4SXZKJIBh2ekamhD6UwCcfe0V9ap"
  callback_url={window.location.origin}
  logout_url={window.location.origin}
>
  <div class="app-container">
    <TopAppBar variant="static" class="top-app-bar">
      <Row style="max-width: 850px;">
        <Section style="padding: 0">
          <Icon class="material-icons">
            <a href="/" rel=prefetch>
                <img src="logo.svg" style="width:40px;height:40px;padding-left: 12px" alt="thinking face" />
            </a>
          </Icon>
          <Title component={A} href="/" rel=prefetch class="mdc-theme--primary" style="padding-left: 8px">
            Bad Decision Maker
          </Title>
        </Section>
        <Section align="end" toolbar>
          <IconButton on:click='{() => !$isAuthenticated ? login(false) : menu.setOpen(true) }'>
            <Icon>
            {#if !$userInfo || !$userInfo.picture}
              <svg style="width:24px;height:24px" viewBox="0 0 24 24">
                <path fill="currentColor" d="{mdiAccountCircleOutline}" />
              </svg>
            {:else}
              <img alt="user picture" style="width:24px;height:24px;border-radius: 50%;" src="{$userInfo.picture}" />
            {/if}
            </Icon>
            <Menu bind:this={menu} anchorCorner="BOTTOM_LEFT">
              <List>
                <Item on:SMUI:action={() => logout()}><Text>Logout</Text></Item>
              </List>
            </Menu>
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

  import { onMount, onDestroy } from 'svelte';
  import TopAppBar, {Row, Section, Title} from '@smui/top-app-bar';
  import A from '@smui/common/A.svelte';
  import IconButton from '@smui/icon-button';
  import {Icon} from '@smui/common';
  import WebFont from 'webfontloader';
  import Menu from '@smui/menu';
  import List, {Item, Separator, Text} from '@smui/list';

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

  let menu;
  let timer;
  let darkMode = null;

  function pickColors() {
    if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) {
      if (!darkMode) {
        darkMode = true;
      }
      else {
        return;
      }
    }
    else if (darkMode) {
      darkMode = false;
    }
    else {
      return;
    }

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
      '#fcea10',
      '#ffda00',
      '#f39200',
      '#e94e1b',
      '#e6332a',
      '#e30613',
      '#be1622'
    ];

    const bifDarkModeTextColors = [
      '#009c9b',
      '#31a936',
      '#9db41f',
      '#f39200',
      '#e94e1b'
    ];

    const bifLightModeTextColors = [
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
      '#e30613',
      '#be1622'
    ];

    document
      .documentElement
      .style
      .setProperty('--mdc-theme-secondary',
        bifColors[Math.floor(Math.random() * bifColors.length)]);

    if (darkMode) {
      document
        .documentElement
        .style
        .setProperty('--mdc-theme-primary',
          bifDarkModeTextColors[Math.floor(Math.random() * bifDarkModeTextColors.length)]);
    }
    else {
      document
        .documentElement
        .style
        .setProperty('--mdc-theme-primary',
          bifLightModeTextColors[Math.floor(Math.random() * bifLightModeTextColors.length)]);
    }

    if (darkMode) {
      document.querySelector('meta[name="apple-mobile-web-app-status-bar-style"]').setAttribute("content", "black-translucent");
      document.querySelector('meta[name="theme-color"]').setAttribute("content", "black");
    }
  }

  onMount(() => {
    WebFont.load({
      google: {
        families: ['Material Icons','Overpass:400,900','Source Sans Pro&display=swap']
      }
    });

    pickColors();
    timer = setInterval(pickColors,1000);
  });

  onDestroy(() => {
    if (timer) {
      clearInterval(timer);
    }
  });
</script>

<style>
.app-container {
  max-width: 850px;
  margin-left: auto;
  margin-right: auto;
}
</style>
