<template>
  <div>
    <h1>TEST</h1>
    <ul class="pokemon-table">
      <li
        class="pokemon-list-item"
        v-for="pokemon in pokemons"
        :key="pokemon.name"
      >
        <PkmnPreview :pokemon="pokemon" />
      </li>
    </ul>
  </div>
</template>

<script>
import PkmnPreview from "./PkmnPreview.vue";
export default {
  name: "PkmnList",
  data() {
    return { pokemons: [] };
  },
  props: ["id", "offset"],
  mounted: function() {
    this.fetchData();
  },
  methods: {
    fetchData: async function() {
      try {
        const result = await fetch(
          `https://pokeapi.co/api/v2/pokemon?limit=${this.id}&offset=${this.offset}`
        );
        const data = await result.json();
        console.log(data);
        this.pokemons = data.results;
      } catch (error) {
        alert(error);
      }
    },
  },
  components: {
    PkmnPreview,
  },
};
</script>

<style>
h1 {
  font-size: 5rem;
  color: white;
}
li {
  color: white;
}
</style>
