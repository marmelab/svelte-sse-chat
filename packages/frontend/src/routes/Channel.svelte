<script>
  import Tchat from "../components/Tchat.svelte";

  export let params = {};
</script>

<style>
  .root {
    padding: 80px 0;
  }
</style>

<div class="root">
  <Tchat channelId={params.id} />
</div>
