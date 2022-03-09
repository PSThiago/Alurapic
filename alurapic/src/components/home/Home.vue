<template>
  <div>
    <h1 class="centralizado">{{ titulo }}</h1>
    <input type="search" class="filtro" @input="filtro = $event.target.value" placeholder="Filtrar por título">
    <ul class="lista-fotos">
      <li class="lista-fotos-item" v-bind:key="foto" v-for="foto of fotosComFiltro">
        <meu-painel :titulo="foto.titulo">
          <imagem-responsiva :url="foto.url" :titulo="foto.titulo"/>
          <meu-botao 
            tipo="button" 
            rotulo="Remover" 
            @botaoAtivado="remove(foto)" 
            :confirmacao="true" 
            estilo="perigo"
          />
        </meu-painel>
      </li>
    </ul>
  </div>
</template>

<script>

  import Painel from '../shared/painel/Painel.vue';
  import ImagemResponsiva from '../shared/imagem-responsiva/ImagemResponsiva.vue';
  import Botao from '../shared/botao/Botao.vue';

  export default {
    components: {
      'meu-painel' : Painel,
      'imagem-responsiva' : ImagemResponsiva,
      'meu-botao' : Botao
    },
    data () {
      return {
        titulo: 'Alurapic',
        filtro: '',
        fotos: []
      }
    }, 

    computed: {

      fotosComFiltro() {
        if(this.filtro) {
          const exp = new RegExp(this.filtro, 'i');
          return this.fotos.filter(foto => exp.test(foto.titulo))
        } else 
          return this.fotos;
      }

    },

    methods: {
      remove(foto) {
        alert("Remover a foto: " + foto.titulo);
      }
    },

    created () {
      this.$http.get("http://localhost:3000/v1/fotos")
        .then(res => res.json())
        .then(fotosJson => this.fotos = fotosJson)
        .catch(err => console.log(err));
    }
  }
</script>

<style>
  
  .centralizado {
    text-align: center;
  }

  .lista-fotos {
    list-style: none;
  }

  .lista-fotos .lista-fotos-item {
    display: inline-block;
  }

  .filtro {
    display: block;
    width: 100%;
  }

</style>
