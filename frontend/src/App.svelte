<script>
  import Router from "svelte-spa-router";
  import LLM from "./lib/LLM.svelte";
  import VoiceReference from "./lib/VoiceReference.svelte";
  import SelectAuthor from "./lib/author_toss/selectAuthor.svelte";

  const routes = {
    "/": LLM,
    "/voice_reference": VoiceReference,
	  "/selectAuthor": SelectAuthor,
  };
</script>

<main>
  <a href="#/">홈</a>
  <a href="#/voice_reference">voice_reference</a>
  <Router {routes} />
</main>
