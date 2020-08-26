<script>
  import { onMount, beforeUpdate, afterUpdate } from "svelte";
  import { querystring } from "svelte-spa-router";

  import { createChannelStore } from "../channel/store";
  import Message from "./Message.svelte";
  import TchatHeader from "./TchatHeader.svelte";
  import TchatInput from "./TchatInput.svelte";

  const getUsername = querystring => {
    const match = querystring.match(/user=([^&]*)/);
    return match ? match[1] : null;
  };

  export let channelId;
  let messages = [];
  let username = getUsername($querystring) || "Unknown";

  let div;
  let autoscroll;

  beforeUpdate(() => {
    autoscroll =
      div && div.offsetHeight + div.scrollTop > div.scrollHeight - 20;
  });

  afterUpdate(() => {
    if (autoscroll) div.scrollTo(0, div.scrollHeight);
  });

  const handleSendMessage = async e => {
    await fetch(`http://localhost:3000/${channelId}/send`, {
      body: JSON.stringify({
        message: e.detail.text,
        username,
        time: Date.now()
      }),
      headers: {
        "Content-Type": "application/json"
      },
      method: "POST"
    });
  };

  onMount(() => {
    const store = createChannelStore(channelId);

    store.subscribe(incomingMessages => {
      messages = incomingMessages;
    });

    return store.close;
  });
</script>

<style>
  .root {
    margin: 0 auto;
    width: 750px;
    border-radius: 5px;
    background: #f2f5f8;
    border-radius: 5px;
    color: #434651;
  }

  .root .history {
    padding: 30px 30px 20px;
    border-bottom: 2px solid white;
    overflow-y: scroll;
    max-height: 375px;
  }

  .root .history ul {
    list-style-type: none;
  }

  .clearfix:after {
    visibility: hidden;
    display: block;
    font-size: 0;
    content: " ";
    clear: both;
    height: 0;
  }
</style>

<div class="root">
  <TchatHeader title={`Chat on ${channelId}`} messageCount={messages.length} />
  <div class="history" bind:this={div}>
    <ul>
      {#each messages as message, i}
        <li class="clearfix">
          <Message alignRight={i % 2} {message} />
        </li>
      {/each}
    </ul>
  </div>
  <TchatInput on:message={handleSendMessage} />
</div>
