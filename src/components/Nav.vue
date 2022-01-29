<template>
  <div class="nav">
    <div class="input-group mb-3">
      <input
        type="number"
        v-model="numero"
        min="1"
        max="150"
        class="form-control"
        placeholder="eliga un numero"
      />
      <button class="btn btn-outline-secondary" @click="enviarNumero">
        Click
      </button>
    </div>
    <div class="input-group mb-3">
      <input v-model="name" type="text" id="" placeholder="eliga un nombre" class="form-control"/>
      <button class="btn btn-outline-secondary" @click="enviarName">
        Click
      </button>
    </div>
  </div>
</template>

<script>
import { ref } from "@vue/runtime-core";
export default {
  setup(props, { emit }) {
    const numero = ref("");
    const name = ref("");

    const enviarNumero = () => {
      emit("enviarNumero", numero.value);
    };

    const enviarName = () => {
      emit("enviarName", name.value);
    };

    return { numero, name, enviarNumero, enviarName };
  },
};
</script>

<style>
</style>