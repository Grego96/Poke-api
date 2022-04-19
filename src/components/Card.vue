<template>
  <div class="principal col-md-3 p-3">
    <!-- {{poke.name}} -->
    <div class="card p-3">
      <div class="head">
        <h3 class="name">{{ pokemon.name }}</h3>
        <p>id: {{pokemon.id}}</p>
      </div>
      <div class="img">
        <img
          class="pokeImg"
          :src="pokemon.sprites?.other?.dream_world?.front_default"
          alt=""
        />
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
  </div>
</template>

<script>
import { ref, watchEffect } from "@vue/runtime-core";

export default {
  props: ["poke"],
  setup(props) {
    var url;
    const pokemon = ref({});

    watchEffect(() => {
      url = props.poke.url;
    });
    const obtenerPokeInfo = async (url) => {
      try {
        const res = await fetch(url);
        const data = await res.json()
        pokemon.value = await data;
      } catch (error) {
        console.log(error);
      }
    };
    obtenerPokeInfo(url);

    return {pokemon};
  },
};
</script>

<style>
.principal {
  width: 100%;
}
.name {
  text-transform: capitalize;
}
.card {
  background: rgb(163,233,161);
background: linear-gradient(90deg, rgba(163,233,161,1) 0%, rgba(66,66,66,0.9051995798319328) 0%, rgba(71,14,14,0.5214460784313726) 100%);
  border-radius: 30px !important;
  border: 5px solid rgb(126, 86, 86) !important;
}
.img {
  width: 100%;
}

.pokeImg {
  height: 300px;
  width: 100%;
}
</style>