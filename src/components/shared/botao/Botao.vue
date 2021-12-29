<template>
  <buttom @click="disparaAcao()" class="botao" :class="estiloBotao">{{
    rotulo
  }}</buttom>
</template>

<script>
export default {
  props: {
    tipo: {
      required: true,
    },
    rotulo: {
      required: true,
    },
    confirmacao: {
      required: true,
    },
    estilo: {
      required: true,
    },
  },
  methods: {
    disparaAcao() {
      if (this.confirmacao) {
        if (confirm("Confirmar ação?")) {
          this.$emit("botaoAtivado");
        }
        return;
      }
      this.$emit("botaoAtivado");
    },
  },
  computed: {
    estiloBotao() {
      if (this.estilo == "padrao") return "botao-padrao";
      return "botao-perigo";
    },
  },
};
</script>

<style>
.botao {
  display: inline-block;
  padding: 10px;
  border-radius: 5px;
  margin: 10px;
  font-size: 1.2rem;
}

.botao-perigo {
  background: firebrick;
  color: white;
}

.botao-padrao {
  background: darkcyan;
  color: white;
}
</style>
