<script lang="ts">
  import "../app.css";
  import NavBar from "../components/NavBar.svelte";
  let { children } = $props();
</script>

<div class="h-screen w-screen flex justify-center">
  <div class="flex flex-col h-full bg-gray-100 max-w-[430px]">
    {@render children()}
    <NavBar />
  </div>
</div>
