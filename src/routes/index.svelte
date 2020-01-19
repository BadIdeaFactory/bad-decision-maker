<svelte:head>
  <title>Bad Decision Maker</title>
</svelte:head>

<section>
  <!--
  <div class="paper-container">
    <a href="/create" rel=prefetch>
      <Paper color="primary" class="paper">
        <Title>Make bad decisions faster</Title>
        <Content>Never before has it been this easy to commit to terrible ideas.</Content>
      </Paper>
    </a>
  </div>
  -->

  <div class="card-container">
    <Card>
      <Content class="mdc-typography--body2">
        <h2 class="mdc-typography--headline6" style="margin: 0;">Poll title</h2>
        <h3 class="mdc-typography--subtitle2" style="margin: 0 0; color: #888;font-size: 15px">Created by slifty yesterday</h3>
        <!--
        It's all in this card. It's a veritable smorgasbord of card features.
        -->
      </Content>
      <a href="/vote" rel=prefetch>
        <Actions fullBleed>
          <Button>
            <Label>Vote</Label>
            <i class="material-icons" aria-hidden="true">arrow_forward</i>
          </Button>
        </Actions>
      </a>
    </Card>
  </div>

  <div class="card-container">
    <Card>
      <Content class="mdc-typography--body2">
        <h2 class="mdc-typography--headline6" style="margin: 0;">Poll title</h2>
        <h3 class="mdc-typography--subtitle2" style="margin: 0 0; color: #888;font-size: 15px">Created by slifty yesterday</h3>
        <!--
        <h3 class="mdc-typography--subtitle2" style="margin: 0 0 10px; color: #888;">And a subtitle.</h3>
        It's all in this card. It's a veritable smorgasbord of card features.
        -->
      </Content>
      <a href="/vote" rel=prefetch>
        <Actions fullBleed>
          <Button>
            <Label>Vote</Label>
            <i class="material-icons" aria-hidden="true">arrow_forward</i>
          </Button>
        </Actions>
      </a>
    </Card>
  </div>

  <div class="card-container">
    <Card>
      <Content class="mdc-typography--body2">
        <h2 class="mdc-typography--headline6" style="margin: 0;">Poll title</h2>
        <h3 class="mdc-typography--subtitle2" style="margin: 0 0; color: #888;font-size: 15px">Created by slifty yesterday</h3>
        <!--
        <h3 class="mdc-typography--subtitle2" style="margin: 0 0 10px; color: #888;">And a subtitle.</h3>
        It's all in this card. It's a veritable smorgasbord of card features.
        -->
      </Content>
      <a href="/vote" rel=prefetch>
        <Actions fullBleed>
          <Button>
            <Label>Vote</Label>
            <i class="material-icons" aria-hidden="true">arrow_forward</i>
          </Button>
        </Actions>
      </a>
    </Card>
  </div>

  <div class="card-container">
    <Card>
      <Content class="mdc-typography--body2">
        <h2 class="mdc-typography--headline6" style="margin: 0;">Poll title</h2>
        <h3 class="mdc-typography--subtitle2" style="margin: 0 0; color: #888;font-size: 15px">Created by slifty yesterday</h3>
        <!--
        <h3 class="mdc-typography--subtitle2" style="margin: 0 0 10px; color: #888;">And a subtitle.</h3>
        It's all in this card. It's a veritable smorgasbord of card features.
        -->
      </Content>
      <a href="/vote" rel=prefetch>
        <Actions fullBleed>
          <Button>
            <Label>Vote</Label>
            <i class="material-icons" aria-hidden="true">arrow_forward</i>
          </Button>
        </Actions>
      </a>
    </Card>
  </div>
  <Fab/>
</section>

<script>
  // import Paper, {Title, Subtitle, Content} from '@smui/paper';
  import Fab from '../components/fab.svelte';
  import Card, {Content, PrimaryAction, Media, MediaContent, Actions, ActionButtons, ActionIcons} from '@smui/card';
  import Button, { Label } from '@smui/button';
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
