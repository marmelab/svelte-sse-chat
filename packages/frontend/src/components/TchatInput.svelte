<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();
  let value = "";

  const handleSubmit = () => {
    dispatch("message", { text: value });

    value = "";
  };
</script>

<style>
  .root {
    padding: 30px;
  }

  .root:after {
    visibility: hidden;
    display: block;
    font-size: 0;
    content: " ";
    clear: both;
    height: 0;
  }

  textarea {
    width: 100%;
    border: none;
    padding: 10px 20px;
    font: 14px/22px "Lato", Arial, sans-serif;
    margin-bottom: 10px;
    border-radius: 5px;
    resize: none;
  }

  button {
    float: right;
    color: #94c2ed;
    font-size: 16px;
    text-transform: uppercase;
    border: none;
    cursor: pointer;
    font-weight: bold;
    background: #f2f5f8;
  }

  button:hover {
    color: #75b1e8;
  }
</style>

<div class="root">
  <textarea bind:value placeholder="Type your message" rows="3" />
  <button on:click={handleSubmit}>Send</button>
</div>
