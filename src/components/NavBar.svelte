<script lang="ts">
  import IconGiftRegular from "phosphor-icons-svelte/IconGiftRegular.svelte";
  import IconQrCodeRegular from "phosphor-icons-svelte/IconQrCodeRegular.svelte";
  import IconStorefrontRegular from "phosphor-icons-svelte/IconStorefrontRegular.svelte";
  import IconHouseRegular from "phosphor-icons-svelte/IconHouseRegular.svelte";
  import IconUserRegular from "phosphor-icons-svelte/IconUserRegular.svelte";
</script>

<div
  class="flex justify-between items-center px-6 py-4 bg-white border-t border-gray-200"
>
  <a class="flex flex-col items-center" href="/home">
    <IconHouseRegular class="text-4xl text-[#B4B4B4]" />
  </a>

  <a class="flex flex-col items-center" href="/stores">
    <IconStorefrontRegular class="text-4xl text-[#B4B4B4]" />
  </a>

  <a class="flex flex-col items-center" href="/pay">
    <IconQrCodeRegular class="text-4xl text-[#B4B4B4]" />
  </a>

  <a class="flex flex-col items-center" href="/egift">
    <IconGiftRegular class="text-4xl text-[#B4B4B4]" />
  </a>

  <a class="flex flex-col items-center" href="/account">
    <IconUserRegular class="text-4xl text-[#B4B4B4]" />
  </a>
</div>
