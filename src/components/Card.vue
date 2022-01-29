<template>
  <div class="principal">
    <div class="cardd">
      <h3 class="name">{{ pokemon.name }}</h3>
      <p>base experience: {{ pokemon.base_experience }}</p>
      <!-- <img
        class="pokeImg"
        :src="pokemon.sprites.other.dream_world.front_default"
        alt=""
      /> -->
    </div>
    <div class="datos">
      <div class="abilities">
        <h3>Abilities</h3>
        <ul>
          <li v-for="(abili, index) in pokemon.abilities" :key="index">
            {{ abili.ability.name }}
          </li>
        </ul>
      </div>
      <div class="tipo">
        <h3>Type:</h3>
        <p v-for="(type, index) in pokemon.types" :key="index">
          {{ type.type.name }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import { inject } from "@vue/runtime-core";
export default {
  setup() {
    const pokemon = inject("pokemonById");
    console.log(pokemon);
    setTimeout(() => {
      console.log(pokemon);
    },5000)

    return { pokemon };
  },
};
</script>

<style>
.name {
  text-transform: capitalize;
}
</style>