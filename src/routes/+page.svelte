<script lang="ts">
  import IconCompassRegular from "phosphor-icons-svelte/IconCompassRegular.svelte";
  import HeaderSearch from "../components/HeaderSearch.svelte";
  import RestaurantCard from "../components/RestaurantCard.svelte";
  import IconBowlSteamRegular from "phosphor-icons-svelte/IconBowlSteamRegular.svelte";
  import IconBreadRegular from "phosphor-icons-svelte/IconBreadRegular.svelte";
  import IconCertificateRegular from "phosphor-icons-svelte/IconCertificateRegular.svelte";
  import IconFireRegular from "phosphor-icons-svelte/IconFireRegular.svelte";
  import IconPepperRegular from "phosphor-icons-svelte/IconPepperRegular.svelte";
  import IconCookingPotRegular from "phosphor-icons-svelte/IconCookingPotRegular.svelte";
  import type { Restaurant } from "$lib/restuarants";
  import { vancouverRestaurants as restaurants } from "$lib/restuarants";

  let activeFilter = $state("Explore");
  let filteredRestaurants = $state<Restaurant[]>([]);

  function filterRestaurants(filter: string) {
    activeFilter = filter;

    switch (filter) {
      case "Explore":
        filteredRestaurants = restaurants;
        break;
      case "Featured":
        filteredRestaurants = restaurants.filter((r) => r.featured);
        break;
      case "Popular":
        filteredRestaurants = restaurants.filter((r) => r.popular);
        break;
      case "Hotpot":
        filteredRestaurants = restaurants.filter((r) =>
          r.categories.includes("Hotpot")
        );
        break;
      case "Bakery":
        filteredRestaurants = restaurants.filter((r) =>
          r.categories.includes("Bakery")
        );
        break;
      case "Noodles":
        filteredRestaurants = restaurants.filter((r) =>
          r.categories.includes("Noodles")
        );
        break;
      case "Szechuan":
        filteredRestaurants = restaurants.filter((r) =>
          r.categories.includes("Szechuan")
        );
        break;
      default:
        filteredRestaurants = restaurants;
    }
  }

  const navCategories = [
    { name: "Explore", icon: IconCompassRegular },
    { name: "Featured", icon: IconCertificateRegular },
    { name: "Popular", icon: IconFireRegular },
    { name: "Hotpot", icon: IconCookingPotRegular },
    { name: "Bakery", icon: IconBreadRegular },
    { name: "Noodles", icon: IconBowlSteamRegular },
    { name: "Szechuan", icon: IconPepperRegular },
  ];

  $effect(() => {
    filterRestaurants(activeFilter);
  });
</script>

<HeaderSearch />

<div
  class="flex space-x-[35px] items-center px-6 py-4 overflow-x-auto border-b border-gray-200"
>
  {#each navCategories as category}
    <!-- svelte-ignore a11y_click_events_have_key_events -->
    <!-- svelte-ignore a11y_no_static_element_interactions -->
    <div
      class="flex flex-col items-center cursor-pointer"
      onclick={() => filterRestaurants(category.name)}
    >
      <category.icon
        class="text-4xl {activeFilter === category.name
          ? 'text-teal-500'
          : 'text-[#B4B4B4]'}"
      />
      <span
        class="text-xs {activeFilter === category.name
          ? 'text-teal-500 font-medium'
          : 'text-gray-400'} mt-1"
      >
        {category.name}
      </span>
    </div>
  {/each}
</div>

<div class="flex-1 overflow-y-auto p-4 space-y-6">
  {#if filteredRestaurants.length === 0}
    <div class="text-center py-10 text-gray-500">
      No restaurants found in this category.
    </div>
  {:else}
    {#each filteredRestaurants as restaurant}
      <RestaurantCard
        address={restaurant.address}
        discount={restaurant.discount || ""}
        restaurantName={restaurant.name}
        logoImg={restaurant.logoImg}
        thumbnail={restaurant.thumbnail}
      >
        {#if restaurant.badge}
          <div class="{restaurant.badge.bgColor} py-3 px-4">
            <div class="{restaurant.badge.textColor} text-sm">
              {restaurant.badge.text}
            </div>
            {#if restaurant.badge.subtext}
              <div class="{restaurant.badge.textColor} text-xl font-bold">
                {restaurant.badge.subtext}
              </div>
            {/if}
          </div>
        {/if}
      </RestaurantCard>
    {/each}
  {/if}
</div>
