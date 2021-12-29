<template>
  <div>
    <h1 class="centralizado">{{ titulo }}</h1>

    <input
      type="search"
      @input="filtro = $event.target.value"
      class="filtro"
      placeholder="filtre pelo título"
    />

    <ul class="lista-fotos">
      <li
        class="lista-fotos--item"
        v-for="foto of fotosFiltradas"
        :key="foto.titulo"
      >
        <meu-painel :titulo="foto.titulo">
          <imagem-responsiva :foto="foto" />
          <meu-botao
            :confirmacao="true"
            tipo="button"
            rotulo="REMOVER"
            estilo="perigo"
            @botaoAtivado="remove(foto)"
          ></meu-botao>
        </meu-painel>
      </li>
    </ul>
  </div>
</template>

<script>
import Painel from "../shared/painel/Painel.vue";
import ImagemResponsiva from "../shared/imagem-responsiva/ImagemResponsiva.vue";
import Botao from "../shared/botao/Botao.vue";

export default {
  components: {
    "meu-painel": Painel,
    "imagem-responsiva": ImagemResponsiva,
    "meu-botao": Botao,
  },
  data() {
    return {
      titulo: "Alurapic",
      fotos: [],
      filtro: "",
    };
  },
  computed: {
    fotosFiltradas() {
      return this.fotos.filter((foto) => {
        return foto.titulo.toLowerCase().includes(this.filtro.toLowerCase());
      });
    },
  },
  methods: {
    remove(foto) {
      console.log(foto);
    },
  },
  created() {
    let promise = this.$http.get("http://localhost:3000/v1/fotos");
    promise
      .then((res) => res.json())
      .then(
        (fotos) => {
          this.fotos = fotos;
        },
        (err) => {
          console.log(err);
        }
      );
  },
};
</script>

<style>
.centralizado {
  text-align: center;
}

.lista-fotos {
  list-style: none;
}

.lista-fotos .lista-fotos--item {
  display: inline-block;
}

.filtro {
  display: block;
  width: 100%;
}
</style>
