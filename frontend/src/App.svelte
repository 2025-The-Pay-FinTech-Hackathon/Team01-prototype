<!-- App.svelte -->
<script lang="ts">
  import Router from 'svelte-spa-router';
  import Home from './lib/Home.svelte';
  import LLM from './lib/LLM.svelte';

  const routes = {
    '/':           Home,
    '/LLM':        LLM,
  };
  import background from './assets/background.png'

</script>

<main class="w-screen h-screen flex">
  <nav class="flex-1 flex flex-col items-center justify-center space-y-6 bg-gray-50">
    <a href="#/" class="text-xl hover:underline">홈</a>
    <a href="#/LLM" class="text-xl hover:underline">채팅</a>
  </nav>

  <div class="flex-1 flex items-center justify-center bg-[url(/assets/images/background.png)] bg-center rounded-3xl">
    <Router {routes} useHash let:Component>
      <div class="w-[360px] h-[640px] bg-white border rounded-3xl shadow-lg p-4 flex flex-col">
        <svelte:component this={Component} />
      </div>
    </Router>
  </div>

  <div class="flex-1 flex items-center justify-center bg-gray-50">
    pintech-team01
  </div>
</main>

<style>
  a { color: #333; text-decoration: none; }
</style>
