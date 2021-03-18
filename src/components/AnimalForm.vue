<template>
<div>
  <h1>Add Animal</h1>
  <form @submit.prevent="addAnimal">
    <label for="species">Species:</label>
    <input
      required
      v-model="species"
      id="species"
      type="text"
      placeholder="species"
    />
    <br />
    <label for="name">Name:</label>
    <input required v-model="name" id="name" type="text" placeholder="name" />
    <br />
    <label for="date">Date:</label>
    <input v-model="date" id="date" type="date" />
    <br />
    <label for="sector">Sector:</label>
    <select required v-model="sector">
      <option v-for="(sector, index) in sectors" :key="index">
        {{ sector }}
      </option>
    </select>
    <br />
    <button type="submit">Add Animal</button>
  </form>
</div>
</template>

<script>
export default {
  name: "AnimalForm",
  props: ["sectors"],
  data() {
    return {
      species: "",
      name: "",
      date: "",
      sector: "",
    };
  },
  methods: {
    addAnimal() {
      this.$emit("add-animal", {
        species: this.species,
        name: this.name,
        date: new Date(this.date),
        sector: this.sector,
      });
      this.species = "";
      this.name = "";
      this.date = "";
      this.sector = "";
    },
  },
};
</script>

<style>
#app input {
  font: inherit;
  padding: 0.15rem;
  
}
#app label {
  font-weight: bold;
  margin-right: 1rem;
  width: 4rem;
  display: inline-block;
}
#app form div {
  margin: 1rem 0;
}
</style>