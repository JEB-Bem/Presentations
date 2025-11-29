<template>
    <Frankfurt />
    <img
      src="./assets/logo.png"
      class="fixed left-3 bottom-3 z-50 select-none"
      style="width: 120px; height: auto;"
    />
    <!--
    <img
      src="./assets/building.png"
      class="fixed right-3 bottom-3 z-50 select-none"
      style="width: 120px; height: auto;"
    />
    -->
	<InfoLine v-if="$slidev.configs.infoLine ?? true" />
</template>
