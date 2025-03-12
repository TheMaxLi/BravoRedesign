<script lang="ts">
  import type { Restaurant } from "$lib/restuarants";
  import { vancouverRestaurants as restaurants } from "$lib/restuarants";
  import IconMagnifyingGlassRegular from "phosphor-icons-svelte/IconMagnifyingGlassRegular.svelte";
  import { page } from "$app/state";
  import { goto } from "$app/navigation";

  let activeFilter = $state("Nearby");
  let filteredRestaurants = $state<Restaurant[]>([]);
  let search = $state<string>(page.url.searchParams.get("search") || "");

  const filters = ["Nearby", "Latest", "Popular", "Top Rewards"] as const;
  $effect(() => {
    filteredRestaurants = filterRestaurants(restaurants, activeFilter, search);
    goto(`/stores?search=${search}`, { replaceState: false, keepFocus: true });
  });

  function filterRestaurants(
    restaurants: Restaurant[],
    filter: string,
    value: string
  ) {
    restaurants = restaurants.filter((r) =>
      r.name.toLowerCase().includes(value.toLocaleLowerCase())
    );
    switch (filter) {
      case "Popular":
        return restaurants.filter((r) => r.popular);
      case "Top Rewards":
        return [...restaurants].sort((a, b) => {
          const aPoints = a.discount?.includes("X Points")
            ? parseInt(a.discount.split("X")[0])
            : 0;
          const bPoints = b.discount?.includes("X Points")
            ? parseInt(b.discount.split("X")[0])
            : 0;
          return bPoints - aPoints;
        });
      case "Latest":
        return [...restaurants].sort((a, b) => b.new - a.new);
      case "Nearby":
      default:
        return restaurants;
    }
  }

  function getRandomDistance() {
    return (Math.random() * 4 + 0.5).toFixed(1);
  }
</script>

<div class="sticky top-0 bg-white shadow-sm z-10">
  <div class="p-4">
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

  <div class="px-4 pb-4 overflow-x-auto flex gap-2 scrollbar-hide">
    {#each filters as filter}
      <button
        class={`px-4 py-2 rounded-full text-sm font-medium whitespace-nowrap transition-all duration-200 ${activeFilter === filter ? "bg-teal-500 text-white" : "bg-gray-200 text-gray-700"}`}
        onclick={() => (activeFilter = filter)}
      >
        {filter}
      </button>
    {/each}

    <!-- Refresh Button -->
    <!-- svelte-ignore a11y_consider_explicit_label -->
    <button class="ml-2 p-2 rounded-full bg-gray-200 text-gray-700">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-5 w-5"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15"
        />
      </svg>
    </button>
  </div>
</div>

<div class="px-4 py-4 pb-[80px] space-y-5 overflow-y-auto">
  {#each filteredRestaurants as restaurant}
    <div class="bg-white rounded-lg overflow-hidden shadow-md">
      <div class="relative h-48 overflow-hidden">
        <div class="flex h-full">
          <div class="w-full h-full bg-gray-200">
            <img
              src={restaurant.thumbnail}
              alt={restaurant.name}
              class="w-full h-full object-cover"
            />
          </div>
        </div>

        {#if restaurant.badge && (restaurant.badge.text || restaurant.badge.subtext)}
          <div
            class={`absolute top-3 left-3 px-3 py-1 rounded-lg ${restaurant.badge.bgColor} ${restaurant.badge.textColor} shadow-lg`}
          >
            {#if restaurant.badge.text}
              <div class="text-xs">{restaurant.badge.text}</div>
            {/if}
            {#if restaurant.badge.subtext}
              <div class="font-bold text-sm">{restaurant.badge.subtext}</div>
            {/if}
          </div>
        {/if}

        <div
          class="absolute bottom-3 right-3 bg-white bg-opacity-90 rounded-lg p-2 shadow"
        >
          <div class="flex items-center space-x-1 text-gray-500">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-4 w-4"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"
              />
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"
              />
            </svg>
            <span class="text-xs font-medium">{getRandomDistance()} km</span>
          </div>
        </div>
      </div>

      <div class="p-4">
        <div class="flex justify-between items-start">
          <div>
            <h3 class="font-bold text-lg text-gray-800">{restaurant.name}</h3>
            <p class="text-sm text-gray-500 mt-1">{restaurant.address}</p>
          </div>

          <div class="flex flex-col items-end">
            <span class="text-xs text-gray-500 mt-1"
              >{(restaurant.totalUsers || 0).toLocaleString()} reviews</span
            >
          </div>
        </div>

        {#if restaurant.discount}
          <div class="pt-3">
            <div class="flex items-center gap-2 overflow-x-auto pb-1">
              {#if restaurant.discount.includes("X Points")}
                <div
                  class="flex items-center bg-teal-50 border border-teal-200 text-teal-600 rounded-lg py-1 px-3 whitespace-nowrap"
                >
                  <div
                    class="w-6 h-6 bg-teal-500 rounded-full flex items-center justify-center mr-2"
                  >
                    <span class="text-white text-xs font-bold"
                      >{restaurant.discount.split(" ")[0]}</span
                    >
                  </div>
                  <span class="text-sm font-medium">PTS Reward</span>
                </div>
              {/if}

              {#if restaurant.discount.includes("off")}
                {#each restaurant.discount.split("•").slice(1) as discount}
                  <div
                    class="flex items-center bg-red-50 border border-red-200 text-red-600 rounded-lg py-1 px-3 whitespace-nowrap"
                  >
                    <svg
                      xmlns="http://www.w3.org/2000/svg"
                      class="h-4 w-4 mr-1"
                      fill="none"
                      viewBox="0 0 24 24"
                      stroke="currentColor"
                    >
                      <path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="2"
                        d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
                      />
                    </svg>
                    <span class="text-sm font-medium">{discount}</span>
                  </div>
                {/each}
              {/if}
            </div>
          </div>
        {/if}
      </div>
    </div>
  {/each}
</div>
