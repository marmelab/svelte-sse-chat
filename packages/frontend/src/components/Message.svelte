<script>
  export let alignRight = false;
  export let message = {
    username: "Unknown",
    message: "",
    time: Date.now()
  };
</script>

<style>
  .root {
    margin-bottom: 15px;
  }

  .time {
    color: #a8aab1;
    padding-left: 6px;
  }

  .message {
    color: white;
    padding: 18px 20px;
    line-height: 26px;
    font-size: 16px;
    border-radius: 7px;
    margin-bottom: 30px;
    width: 90%;
    position: relative;
  }

  .message:after {
    bottom: 100%;
    left: 7%;
    border: solid transparent;
    content: " ";
    height: 0;
    width: 0;
    position: absolute;
    pointer-events: none;
    border-bottom-color: #86bb71;
    border-width: 10px;
    margin-left: -10px;
  }

  .my-message {
    background: #86bb71;
  }

  .other-message {
    background: #94c2ed;
  }

  .other-message:after {
    border-bottom-color: #94c2ed;
    left: 93%;
  }

  .online,
  .me {
    margin-right: 3px;
    font-size: 10px;
  }

  .online {
    color: #86bb71;
  }

  .me {
    color: #94c2ed;
  }

  .align-right {
    text-align: right;
  }
  .float-right {
    float: right;
  }
</style>

{#if alignRight}
  <div>
    <div class="root align-right">
      <span class="time">
        {`${new Date(message.time).toLocaleDateString()} ${new Date(message.time).toLocaleTimeString()}`}
      </span>
      &nbsp; &nbsp;
      <span>{message.username}</span>
      <i class="fa fa-circle me" />
    </div>
    <div class="message other-message float-right">{message.message}</div>
  </div>
{:else}
  <div>
    <div class="root">
      <span>
        <i class="fa fa-circle online" />
        {message.username}
      </span>
      <span class="time">
        {`${new Date(message.time).toLocaleDateString()} ${new Date(message.time).toLocaleTimeString()}`}
      </span>
    </div>
    <div class="message my-message">{message.message}</div>
  </div>
{/if}
