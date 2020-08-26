<script>
  import Router from "svelte-spa-router";
  import Home from "./routes/Home.svelte";
  import Channel from "./routes/Channel.svelte";

  const routes = {
    "/": Home,
    "/channel/:id": Channel
  };
</script>

<Router {routes} />
