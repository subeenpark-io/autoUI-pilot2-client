<script>
  import { Router, Route } from "svelte-routing";
  import Home from "../components/Home.svelte";
  import Thanks from "../components/Thanks.svelte";
  import Blog from "../components/Blog.svelte";
  import Before from "../components/Before.svelte";
  import After from "../components/After.svelte";
  import PostHoc from "../components/PostHoc.svelte";

  export let url = "";
</script>

<Router {url}>
  <div>
    <Route path="blog" component={Blog} />
    <Route path="thanks" component={Thanks} />
    <Route path="/" component={Home} />
    <Route path="before" component={Before} />
    <Route path="after" component={After} />
    <Route path="posthoc" component={PostHoc} />
  </div>
</Router>
