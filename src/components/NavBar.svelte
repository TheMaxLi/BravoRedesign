<script lang="ts">
  import IconGiftRegular from "phosphor-icons-svelte/IconGiftRegular.svelte";
  import IconQrCodeRegular from "phosphor-icons-svelte/IconQrCodeRegular.svelte";
  import IconStorefrontRegular from "phosphor-icons-svelte/IconStorefrontRegular.svelte";
  import IconHouseRegular from "phosphor-icons-svelte/IconHouseRegular.svelte";
  import IconUserRegular from "phosphor-icons-svelte/IconUserRegular.svelte";
  import { page } from "$app/state";
</script>

<div
  class="fixed bottom-0 w-full flex justify-between items-center px-6 py-4 bg-white border-t border-gray-200"
>
  <a class="flex flex-col items-center" href="/">
    <IconHouseRegular
      class="text-4xl  {page.url.pathname === '/'
        ? 'text-teal-500'
        : 'text-[#B4B4B4]'}"
    />
  </a>

  <a class="flex flex-col items-center" href="/stores">
    <IconStorefrontRegular
      class="text-4xl  {page.url.pathname === '/stores'
        ? 'text-teal-500'
        : 'text-[#B4B4B4]'}"
    />
  </a>

  <div class="flex flex-col items-center">
    <IconQrCodeRegular class="text-4xl text-[#B4B4B4]" />
  </div>

  <div class="flex flex-col items-center">
    <IconGiftRegular class="text-4xl text-[#B4B4B4]" />
  </div>

  <div class="flex flex-col items-center">
    <IconUserRegular class="text-4xl text-[#B4B4B4]" />
  </div>
</div>
