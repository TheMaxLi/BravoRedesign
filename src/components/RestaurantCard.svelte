<script lang="ts">
  import type { Snippet } from "svelte";

  let {
    thumbnail,
    discount,
    restaurantName,
    logoImg,
    address,
    children,
  }: {
    thumbnail: string;
    discount: string;
    restaurantName: string;
    logoImg: string;
    address: string;
    children: Snippet;
  } = $props();
</script>

<div class="rounded-3xl overflow-hidden shadow-lg">
  <div class="relative">
    <img
      src={thumbnail}
      alt="{restaurantName} Thumbnail"
      class="w-full h-48 object-cover"
    />
    <div
      class="absolute top-4 left-4 bg-white rounded-full px-4 py-1 text-sm text-teal-600 font-medium"
    >
      {discount}
    </div>
  </div>

  <div class="bg-white p-4">
    <div class="flex items-center">
      <div
        class="w-16 h-16 bg-white rounded-full flex items-center justify-center border-2 border-gray-200"
      >
        <img
          src={logoImg}
          alt="{restaurantName} logo"
          class="w-12 h-12 object-contain rounded-full"
        />
      </div>
      <div class="ml-4">
        <h3 class="text-xl font-bold">{restaurantName}</h3>
        <p class="text-gray-600 text-sm">
          {address}
        </p>
      </div>
    </div>
  </div>

  {@render children()}
</div>
