<template>
  <div class="pkmn-container">
    <h1 class="poke-name">{{ pokemon.name }}</h1>
    <img :src="sprite" alt="" />
  </div>
</template>

<script>
export default {
  name: "PkmnPreview",
  props: ["pokemon"],
  data() {
    return {
      SinglePokemon: {},
    };
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    fetchData: async function() {
      try {
        console.log(this.pokemon);

        const result = await fetch(`${this.pokemon.url}`);
        const SinglePokemon = await result.json();
        this.SinglePokemon = SinglePokemon;
      } catch (error) {
        console.log(error);
      }
    },
  },
  computed: {
    sprite: function() {
      return `https://pokeres.bastionbot.org/images/pokemon/${this.SinglePokemon.id}.png`;
      //return this.SinglePokemon.sprites.front_default;
    },
  },
};
</script>

<style lang="scss">
#query {
  color: #111;
  font-size: 2rem;
}
.pkmn-container {
  background-color: #999;
  padding: 2rem;
  color: #111;
}
.poke-name {
  font-size: 2rem;
}
</style>
