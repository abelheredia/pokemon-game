<template>
  <h1 v-if="!pokemon">Espere por favor ...</h1>
  <div v-else>
    <h1>¿Quién es este pokémon?</h1>
    <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon" />
    <PokemonOptions :pokemons="pokemons" @selection="checkAnswer($event)" />
    <div v-if="showAnswer">
      <h2>{{ message }}</h2>
      <button @click="reset">Nuevo Juego</button>
    </div>
  </div>
  <h2 class="puntaje">Puntaje: {{ puntaje }}</h2>
</template>

<script>
import PokemonPicture from "../components/PokemonPicture.vue";
import PokemonOptions from "../components/PokemonOptions.vue";

import getPokemonOptions from "@/helpers/getPokemonOptions";

getPokemonOptions();

export default {
  components: { PokemonPicture, PokemonOptions },
  data() {
    return {
      pokemons: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: "",
      puntaje: 0,
    };
  },
  methods: {
    async mixPokemonArray() {
      this.pokemons = await getPokemonOptions();
      const rndInt = Math.floor(Math.random() * this.pokemons.length);
      this.pokemon = this.pokemons[rndInt];
    },
    checkAnswer(pokemonId) {
      this.showPokemon = true;
      this.showAnswer = true;

      if (pokemonId === this.pokemon.id) {
        this.message = `Correcto! ${this.pokemon.name} es el pokémon`;
        this.puntaje++;
      } else {
        this.message = `Incorrecto! ${this.pokemon.name} es el pokémon`;
      }
    },
    reset() {
      this.showPokemon = false;
      this.showAnswer = false;
      this.pokemons = [];
      this.pokemon = null;
      this.mixPokemonArray();
    },
    reset2() {
      this.showPokemon = false;
      this.showAnswer = false;
      this.pokemons = [];
      this.pokemon = null;
      this.mixPokemonArray();
    },
  },
  mounted() {
    this.mixPokemonArray();
  },
};
</script>

<style scoped>
.intentos {
  position: absolute;
  top: 0;
  right: 10rem;
}
.puntaje {
  position: absolute;
  top: 3.5rem;
  right: 10rem;
}
</style>
