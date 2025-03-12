<script lang="ts">
  import IconMagnifyingGlassRegular from "phosphor-icons-svelte/IconMagnifyingGlassRegular.svelte";

  let { search = $bindable() } = $props();
</script>

<div class="bg-[#53B5C2] p-4 rounded-b-3xl shadow-md">
  <div class="relative">
    <input
      type="text"
      placeholder="Search"
      bind:value={search}
      class="w-full py-3 px-6 rounded-2xl shadow-md shadow-current bg-white text-gray-400 focus:outline-none text-lg"
    />
    <a class="absolute right-4 top-3" href={`/stores?search=${search}`}>
      <IconMagnifyingGlassRegular class="text-2xl text-[#B4B4B4]" />
    </a>
  </div>
</div>
