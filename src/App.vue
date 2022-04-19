<template>
  <div class="body p-3">
    <div class="row">
      <div class="col-md-2 p-3">
        <Nav
          v-on:enviarNumero="obtenerPokemonsById"
          v-on:enviarName="obtenerPokemonByName"
          v-on:primeros="obtenerPokemons(urlprim)"
          v-on:siguientes="obtenerSiguiente"
          v-on:anterior="obtenerAnterior"
        />
      </div>
      <div class="col-md-10">
        <div class="row">
          <Card
            v-for="(poke, index) in pokeResultado"
            :key="index"
            :poke="poke"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, watchEffect } from "@vue/runtime-core";
import Nav from "./components/Nav.vue";
import Card from "./components/Card.vue";

export default {
  name: "App",
  components: {
    Nav,
    Card,
  },
  setup() {
    const pokeResultado = ref([]),
      pokepoke = ref({
        url: "",
      }),
      urlprim = "https://pokeapi.co/api/v2/pokemon/",
      url = ref(urlprim),
      urlSig = ref(""),
      urlPrev = ref("");

    const obtenerPokemons = async (url) => {
      try {
        pokeResultado.value = [];
        const res = await fetch(url);
        const data = await res.json();
        if ((await data.next) != null) {
          urlSig.value = await data.next;
        } else {
          urlSig.value = url;
        }
        if ((await data.previous) != null) {
          urlPrev.value = await data.previous;
        } else {
          urlPrev.value = url;
        }
        console.log(urlSig);
        pokeResultado.value = await data.results;
        console.log(pokeResultado.value);
      } catch (error) {
        console.log(error);
      }
    };

    const obtenerSiguiente = () => {
      url.value = urlSig.value;
      obtenerPokemons(url.value);
    };

    const obtenerAnterior = () => {
      url.value = urlPrev.value;
      obtenerPokemons(url.value);
    };

    const obtenerPokemonsById = async (id) => {
      try {
        pokeResultado.value = [];
        const url = `https://pokeapi.co/api/v2/pokemon/${id}`;
        const res = await fetch(url);
        const data = await res.json();
        pokepoke.value.url = url;
        pokeResultado.value.push(pokepoke.value);
        console.log(data);
      } catch (error) {
        console.log(error);
      }
    };

    const obtenerPokemonByName = async (name) => {
      try {
        pokeResultado.value = [];
        const url = `https://pokeapi.co/api/v2/pokemon/${name}`;
        const res = await fetch(url);
        const data = await res.json();
        pokepoke.value.url = url;
        pokeResultado.value.push(pokepoke.value);
        console.log(data);
      } catch (error) {
        console.log(error);
      }
    };

    obtenerPokemons(url.value);

    watchEffect(() => {
      console.log(pokeResultado);
    });

    // console.log("hola");
    // console.log(pokeResultado);


    return {
      url,
      urlprim,
      urlSig,
      urlPrev,
      obtenerPokemons,
      obtenerSiguiente,
      obtenerAnterior,
      pokeResultado,
      obtenerPokemonByName,
      obtenerPokemonsById,
    };
  },
};
</script>

<style>
.body {
  /* height: 100vh; */
  display: flex;
  justify-content: center;
  /* align-items: center; */
  background: rgb(163, 233, 161);
  background: linear-gradient(
    90deg,
    rgba(163, 233, 161, 1) 0%,
    rgba(0, 0, 0, 0.9051995798319328) 0%,
    rgba(0, 0, 0, 0.5214460784313726) 100%
  );
  color: white;
}
</style>
