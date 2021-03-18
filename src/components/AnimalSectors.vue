<template>
  <div>
    <h1>Sectors</h1>
    <ul>
      <li v-for="(sector, index) in sectors" :key="index">
        {{ sector }}
        <button @click="emitClick(sector)">Vidi listu zivotinja</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ["sectors"],
  methods: {
    emitClick(sectorToShow) {
      this.$emit("sector-click", sectorToShow);
    },
  },
};
</script>

<style>

</style>