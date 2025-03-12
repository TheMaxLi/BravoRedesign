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
      class="w-full h-72 object-cover"
    />
    <div
      style="background: linear-gradient(to bottom, rgba(31, 41, 55, 0) 0%, rgba(31, 41, 55, 0.6) 40%, rgba(31, 41, 55, 0.8) 100%);"
      class="absolute bottom-0 w-full h-[40%] bg-black"
    ></div>

    <div
      class="absolute top-4 left-4 bg-white rounded-full px-4 py-1 text-sm text-teal-600 font-medium"
    >
      {discount}
    </div>
    <div class="flex items-center p-4 pb-3 absolute bottom-0">
      <div
        class="w-14 h-14 bg-white rounded-full flex items-center justify-center border-2 border-gray-200"
      >
        <img
          src={logoImg}
          alt="{restaurantName} logo"
          class="w-12 h-12 object-contain rounded-full"
        />
      </div>
      <div class="ml-4">
        <h3 class="text-xl font-bold text-white">{restaurantName}</h3>
        <p class="text-white text-sm">
          {address}
        </p>
      </div>
    </div>
  </div>

  {@render children()}
</div>
