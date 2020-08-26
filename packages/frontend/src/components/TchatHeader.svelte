<script>
  export let title = "Chat";
  export let messageCount = 0;
</script>

<style>
  .root {
    padding: 20px;
    border-bottom: 2px solid white;
  }

  .root img {
    float: left;
  }

  .root .about {
    float: left;
    padding-left: 10px;
    margin-top: 6px;
  }

  .root .with {
    font-weight: bold;
    font-size: 16px;
  }

  .root .num-messages {
    color: #92959e;
  }

  .root .fa-star {
    float: right;
    color: #d8dadf;
    font-size: 20px;
    margin-top: 12px;
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

<div class="root clearfix">
  <img
    src="./logo.png"
    alt="avatar"
    width="55" />
  <div class="about">
    <div class="with">{title}</div>
    <div class="num-messages">
      already {messageCount > 1 ? `${messageCount} messages` : `${messageCount} message`}
    </div>
  </div>
  <i class="fa fa-star" />
</div>
