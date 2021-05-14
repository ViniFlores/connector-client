<template>
  <div class="flex fixed items-center justify-center" style="left: 0px; top: 0px; width: 100vw; height: 100vh;">
    <div class="fixed opacity-70 bg-yellow-700" style="width: 100vw; height: 100vh; z-index: 0;" />
    <div style="z-index: 2;">
      <slot />
    </div>
  </div>
</template>

<script>
export default {}
</script>
