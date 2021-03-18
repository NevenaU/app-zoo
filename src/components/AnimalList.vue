<template>
  <div>
    <animal-form @add-animal="addAnimal" :sectors="sectors"></animal-form>
    <hr />
    <h1>Animal List</h1>
    <table style="width: 100%">
      <tr>
        <th>Species</th>
        <th>Name</th>
        <th>Date</th>
        <th>Sector</th>
      </tr>
      <tr
        v-for="({ species, name, date, sector }, index) in animals"
        :key="index"
      >
        <td>{{ species }}</td>
        <td>{{ name }}</td>
        <td>{{ date ? date : "Nepoznat" | moment("MMMM Do YYYY") }}</td>
        <td>{{ sector }}</td>
        <button @click="removeAnimal(index)">Remove</button>
        |
        <button @click="moveToTop(index)">Move</button>
      </tr>
    </table>
    <hr />
    <animal-sectors
      :sectors="sectors"
      @sector-click="showAnimalsForSector"
    ></animal-sectors>
  </div>
</template>

<script>
import AnimalForm from "./AnimalForm";
import AnimalSectors from "./AnimalSectors";
export default {
  components: {
    AnimalForm,
    AnimalSectors,
  },
  data() {
    return {
      sectors: ["Ptice", "Zmije", "Macke", "Bube", "Divlje", "Psi", "Domace"],
      animals: [
        {
          species: "Cat",
          name: "Luna",
          date: new Date(),
          sector: "Macke",
        },
        {
          species: "Dog",
          name: "Bady",
          date: new Date(),
          sector: "Psi",
        },
        {
          species: "Cow",
          name: "Sarulja",
          date: null,
          sector: "Domace",
        },
        {
          species: "Snake",
          name: "Sarulja",
          date: new Date(),
          sector: "Divlje",
        },
        {
          species: "Sheep",
          name: "Zara",
          date: null,
          sector: "Domace",
        },
      ],
    };
  },
  methods: {
    removeAnimal(indexToRemove) {
      this.animals = this.animals.filter(
        (animal, index) => index !== indexToRemove
      );
    },
    moveToTop(indexToMove) {
      const animalToMove = this.animals[indexToMove];
      this.removeAnimal(indexToMove);
      this.animals.unshift(animalToMove);
    },
    addAnimal(newAnimal) {
      this.animals.push(newAnimal);
    },
    showAnimalsForSector(sector) {
				const animalsToShow = this.animals.reduce((acc, current) => {
					if( current.sector === sector){
						acc += " " + current.name
					}
					return acc;
				}, "")
				alert(animalsToShow)
			}
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
* {
  box-sizing: border-box;
}

html {
  font-family: "Jost", sans-serif;
}

body {
  margin: 0;
}

header {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 3rem auto;
  border-radius: 10px;
  padding: 1rem;
  background-color: #58004d;
  color: white;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}

#app ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

#app li,
#app form,
#app table {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 1rem auto;
  border-radius: 10px;
  padding: 1rem;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}

#app h2 {
  font-size: 2rem;
  border-bottom: 4px solid #ccc;
  color: #58004d;
  margin: 0 0 1rem 0;
}

#app button {
  font: inherit;
  cursor: pointer;
  border: 1px solid #ff0077;
  background-color: #ff0077;
  color: white;
  padding: 0.05rem 1rem;
  box-shadow: 1px 1px 2px rgba(0, 0, 0, 0.26);
}

#app button:hover,
#app button:active {
  background-color: #ec3169;
  border-color: #ec3169;
  box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.26);
}
</style>