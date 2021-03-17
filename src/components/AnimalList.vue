<template>
  <div>
    <h1>Animal List</h1>
    <table style="width: 100%">
      <tr>
        <th>Vrsta</th>
        <th>Ime</th>
        <th>Datum</th>
      </tr>
      <tr v-for="({ species, name, date }, index) in animals" :key="index">
			<td>{{species}}</td>
			<td>{{name}}</td>
			<td>{{ date ? date : 'Nepoznat' }}</td>
            <button @click='removeAnimal(index)'>Remove</button>
            <button @click='moveToTop(index)'>Move</button>
		</tr>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      animals: [
        {
          species: "Cat",
          name: "Luna",
          date: new Date(),
        },
        {
          species: "Dog",
          name: "Bady",
          date: new Date(),
        },
        {
          species: "Cow",
          name: "Sarulja",
          date: null,
        },
        {
          species: "Snake",
          name: "Sarulja",
          date: new Date(),
        },
        {
          species: "Sheep",
          name: "Zara",
          date: null,
        },
      ],
    };
  },
  methods: {
      removeAnimal(indexToRemove) {
         this.animals = this.animals.filter((animal, index) => index !== indexToRemove )
      },
      moveToTop(indexToMove) {
        const animalToMove = this.animals[indexToMove]
				this.removeAnimal(indexToMove)
				this.animals.unshift(animalToMove);
      }
  }
};
</script>

<style>
</style>