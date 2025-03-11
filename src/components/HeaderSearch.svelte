<script lang="ts">
  import IconMagnifyingGlassRegular from "phosphor-icons-svelte/IconMagnifyingGlassRegular.svelte";
</script>

<div class="bg-[#53B5C2] p-4 rounded-b-3xl shadow-md">
  <div class="relative">
    <input
      type="text"
      placeholder="Search"
      class="w-full py-3 px-6 rounded-full bg-white text-gray-400 focus:outline-none text-lg"
    />
    <div class="absolute right-4 top-3">
      <IconMagnifyingGlassRegular class="text-2xl text-[#B4B4B4]" />
    </div>
  </div>
</div>
