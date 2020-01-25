<svelte:head>
  <title>Bad Decision Maker</title>
</svelte:head>

<section>
  {#each polls.sort((a,b) => b.createdAt-a.createdAt) as poll}

  <div class="card-container">
    <Card>
      <Content class="mdc-typography--body2">
        <h2 class="mdc-typography--headline6" style="margin: 0;">{poll.title}</h2>
        <h3 class="mdc-typography--subtitle2" style="margin: 0 0; color: #888;font-size: 15px">Created by {poll.creator} <!-- yesterday --></h3>
      </Content>
      <a href="/vote/{poll.id}" rel=prefetch>
        <Actions fullBleed>
          <Button>
            <Label>Vote</Label>
            <i class="material-icons" aria-hidden="true">arrow_forward</i>
          </Button>
        </Actions>
      </a>
    </Card>
  </div>

  {/each}

  <Fab/>
</section>

<script context="module">
  export async function preload(page, session) {
    const res = await this.fetch(`https://xuyhy09bx7.execute-api.us-east-1.amazonaws.com/dev/polls`);
    const polls = await res.json();

    return { polls };
  }
</script>

<script>
  import Fab from '../components/fab.svelte';
  import Card, {Content, PrimaryAction, Media, MediaContent, Actions, ActionButtons, ActionIcons} from '@smui/card';
  import Button, { Label } from '@smui/button';

  export let polls;
</script>

<style>
  a {
    text-decoration: none;
  }

  .card-container {
    margin-left: auto;
    margin-right: auto;
    max-width: 700px;
  }
</style>
