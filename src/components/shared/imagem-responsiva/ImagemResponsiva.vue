<template>
  <img class="imagem-responsiva" :src="foto.url" :alt="foto.titulo" />
</template>

<script>
export default {
  props: ["foto"],
};
</script>

<style>
.imagem-responsiva {
  width: 100%;
}
</style>
