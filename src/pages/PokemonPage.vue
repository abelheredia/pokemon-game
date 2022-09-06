<template>
  <div>
    <h1>¿Quién es este pokémon?</h1>
    <PokemonPicture :pokemonId="1" :showPokemon="true" />
    <PokemonOptions />
  </div>
</template>

<script>
import PokemonPicture from "../components/PokemonPicture.vue";
import PokemonOptions from "../components/PokemonOptions.vue";

export default {
  components: { PokemonPicture, PokemonOptions },
};
</script>
