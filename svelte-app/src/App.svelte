<script>
  import Router from "./routes/index.svelte";
  import "./global.css";
</script>

<!-- <svelte:head>
  <meta
    http-equiv="Content-Security-Policy"
    content="upgrade-insecure-requests"
  />
</svelte:head> -->

<main>
  <Router />
</main>

<style>
  main {
    width: 100vw;
    height: 100vh;
    padding: 0;
    margin: 0;
    display: flex;
    align-items: center;
    justify-content: center;
  }
</style>
