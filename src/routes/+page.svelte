<script lang="ts">
  import IconCompassRegular from "phosphor-icons-svelte/IconCompassRegular.svelte";
  import HeaderSearch from "../components/HeaderSearch.svelte";
  import RestaurantCard from "../components/RestaurantCard.svelte";
  import Featured from "../../static/Featured.svg";
  import FeaturedIcon from "../components/FeaturedIcon.svelte";
</script>

<HeaderSearch />

<!-- Navigation menu -->
<div
  class="flex space-x-[35px] items-center px-6 py-4 overflow-x-auto border-b border-gray-200"
>
  <div class="flex flex-col items-center">
    <IconCompassRegular class="text-5xl text-[#B4B4B4]" />
    <span class="text-sm text-gray-400 mt-1">Explore</span>
  </div>

  <div class="flex flex-col items-center">
    <FeaturedIcon />
    <span class="text-sm text-gray-400 mt-1">Featured</span>
  </div>

  <div class="flex flex-col items-center">
    <IconCompassRegular class="text-5xl text-[#B4B4B4]" />
    <span class="text-sm text-gray-400 mt-1">New</span>
  </div>

  <div class="flex flex-col items-center">
    <IconCompassRegular class="text-5xl text-[#B4B4B4]" />
    <span class="text-sm text-gray-400 mt-1">Popular</span>
  </div>

  <div class="flex flex-col items-center">
    <IconCompassRegular class="text-5xl text-[#B4B4B4]" />
    <span class="text-sm text-gray-400 mt-1">Hotpot</span>
  </div>

  <div class="flex flex-col items-center">
    <IconCompassRegular class="text-5xl text-[#B4B4B4]" />
    <span class="text-sm text-gray-400 mt-1">BBQ</span>
  </div>
</div>

<div class="flex-1 overflow-y-auto p-4 space-y-6">
  <!-- Italian Restaurant Card -->
  <RestaurantCard
    address="780 Thurlow Street (Robson & Alberni St)"
    discount="3X Points • $8 off $100 • $4 off $50"
    restaurantName="CAFE IL NIDO"
    logoImg="https://via.placeholder.com/50"
    thumbnail="https://via.placeholder.com/600x300"
  >
    <div class="bg-purple-700 py-3 px-4">
      <div class="text-white text-sm">Diners' Choice 2024</div>
      <div class="text-white text-xl font-bold">
        Traditional Italian Cuisine since 1988
      </div>
    </div>
  </RestaurantCard>
  <!-- Thai Restaurant Card -->
  <RestaurantCard
    address="Burnaby • 3327 Kingsway"
    discount="8X Points"
    restaurantName="Super Thai DIY Hot Pot"
    logoImg="https://via.placeholder.com/50"
    thumbnail="https://via.placeholder.com/600x300"
  >
    <div class="bg-yellow-500 py-3 px-4">
      <div class="text-yellow-900 text-xl font-bold">NEW TRENDING</div>
    </div>
  </RestaurantCard>
</div>
