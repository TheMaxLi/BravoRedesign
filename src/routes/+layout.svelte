<script lang="ts">
  import "../app.css";
  import NavBar from "../components/NavBar.svelte";
  let { children } = $props();
</script>

<!-- Main app container -->
<div class="flex flex-col h-screen bg-gray-100">
  {@render children()}
  <NavBar />
</div>
