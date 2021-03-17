<template>
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
    <button type="submit">Add Animal</button>
  </form>
</template>

<script>
export default {
    name: "AnimalForm",
	data() {
		return {
			species: "",
			name: "",
			date: "",
		}
	},
    methods: {
		addAnimal() {
			this.$emit('add-animal', {
				species: this.species,
				name: this.name,
				date: new Date(this.date),
			})
			this.species = ""
			this.name = ""
			this.date = ""
		},
       
    }
};
</script>

<style>
</style>