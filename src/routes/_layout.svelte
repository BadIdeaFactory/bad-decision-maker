<Auth0Context domain="zubakskees-dev.auth0.com" client_id="W50D4SXZKJIBh2ekamhD6UwCcfe0V9ap">
  <TopAppBar variant="standard" class="top-app-bar">
    <Row>
      <Section style="padding: 0">
        <Title component={A} href="/" rel=prefetch class="mdc-theme--primary">
          Bad Decision Maker
        </Title>
      </Section>
      <Section align="end" toolbar>
        <IconButton on:click='{() => !$isAuthenticated ? login() : logout() }'>
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
</script>

<style>
.main-content {
  padding-top: 40px;
}
</style>
