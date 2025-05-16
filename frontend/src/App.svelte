<script>
  import Router from "svelte-spa-router";
  import LLM from "./lib/LLM.svelte";
  import SelectAuthor from "./lib/author_toss/selectAuthor.svelte";

  const routes = {
    "/": LLM,
	  "/selectAuthor": SelectAuthor,
  };
</script>

<main>
  <a href="#/">홈</a>
  <Router {routes} />
</main>
