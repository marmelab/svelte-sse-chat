<script>
  import { push } from "svelte-spa-router";

  let channelId = "";
  let username = "";

  const handleJoin = () => {
    push(`/channel/${channelId}?user=${username}`);
  };
</script>

<div>
  <div>
    <span>Channel</span>
    <input bind:value={channelId} type="text" />
  </div>
  <div>
    <span>Username</span>
    <input bind:value={username} type="text" />
  </div>
  <button on:click={handleJoin}>Join !</button>
</div>
