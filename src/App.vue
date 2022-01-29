<template>
  <div class="body">
    <div class="col-md-3 p-5">
      <Nav
        @enviarNumero="obtenerPokemonsById"
        @enviarName="obtenerPokemonByName"
      />
    </div>
    <div class="col-md-9 p-5">
      <Card />
    </div>
  </div>
</template>

<script>
import { provide, ref } from "@vue/runtime-core";
import Nav from "./components/Nav.vue";
import Card from "./components/Card.vue";

export default {
  name: "App",
  components: {
    Nav,
    Card
  },
  setup() {
    let pokemonById = ref({});
    let pokemonByName = ref({});

    const obtenerPokemonsById = async (id) => {
      try {
        const res = await fetch(`https://pokeapi.co/api/v2/pokemon/${id}`);
        const data = await res.json();
        pokemonById.value = await data;
        console.log(data);
      } catch (error) {
        console.log(error);
      }
    };
    const obtenerPokemonByName = async (name) => {
      try {
        const res = await fetch(`https://pokeapi.co/api/v2/pokemon/${name}`);
        const data = await res.json();
        pokemonByName.value = await data;
        console.log(data);
      } catch (error) {
        console.log(error);
      }
    };

    obtenerPokemonsById(1);
    obtenerPokemonByName("bulbasaur");

    provide("pokemonByName", pokemonByName);
    provide("pokemonById", pokemonById);
    
    return {
      obtenerPokemonsById,
      obtenerPokemonByName,
      pokemonById,
      pokemonByName,
    };
  },
};
</script>

<style>
.body {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgb(190, 190, 190);
  background: linear-gradient(
    137deg,
    rgba(190, 190, 190, 1) 0%,
    rgba(133, 181, 152, 1) 100%
  );
}
.principal {
  border-color: 5px solid red;
}
.cardd {
  background-color: rgb(217, 243, 243);
  padding: 50px;
  border-radius: 30px 30px 0 0;
}
.name {
  font-size: 50px;
}
.pokeImg {
  height: 400px;
  width: 400px;
}
.datos {
  background-color: rgb(175, 235, 235);
  padding: 30px;
  border-radius: 0 0 30px 30px;
  display: flex;
  justify-content: space-between;
  height: 180px;
}
.tipo {
  width: 50%;
}
</style>
