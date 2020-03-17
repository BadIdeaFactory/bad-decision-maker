<svelte:head>
  <title>Bad Decision Maker</title>
</svelte:head>

<section>
  {#each polls.sort((a,b) => b.createdAt-a.createdAt) as poll}

  <div class="card-container">
    <Card>
      <a href="/vote/{poll.id}" rel=prefetch>
        <PrimaryAction>
          <Content class="mdc-typography--body2">
            <h2 class="mdc-typography--headline6" style="margin: 0;">{poll.title}</h2>
            <h3 class="mdc-typography--subtitle2" style="margin: 0 0; opacity: 0.8;font-size: 15px">Created by {poll.creator} <!-- yesterday --></h3>
          </Content>
          <Actions fullBleed>
            <Button>
              <Label>Vote</Label>
              <i class="material-icons" aria-hidden="true">arrow_forward</i>
            </Button>
          </Actions>
        </PrimaryAction>
      </a>
    </Card>
  </div>

  {/each}

  <Fab/>
</section>

<script>
  import Fab from '../components/fab.svelte';
  import Card, {Content, PrimaryAction, Media, MediaContent, Actions, ActionButtons, ActionIcons} from '@smui/card';
  import Button, { Label } from '@smui/button';
  import { onMount, onDestroy } from 'svelte';

  let polls = [];

  async function refreshPolls () {
    const res = await fetch(`https://api.baddecisions.app/polls`);
    polls = await res.json();
  }

  onMount(() => {
    refreshPolls();

    //timer = setInterval(refreshPolls,10000);
  });
/*
  onDestroy(() => {
    if (timer) {
      clearInterval(timer);
    }
  });*/
</script>

<style>
  a {
    text-decoration: none;
  }
</style>
