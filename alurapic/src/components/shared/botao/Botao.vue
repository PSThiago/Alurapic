<template>
    <button @click="disparaAcao()" :class="'botao ' + estiloDoBotao" :type="tipo">{{ rotulo }}</button>
</template>

<script>

    export default {
        props: {
            tipo: {
                required: true,
                type: String
            }, 
            rotulo: {
                required: true,
                type: String
            }, 
            confirmacao: Boolean, 
            estilo: String
        },
        methods: {
            disparaAcao() {
                if (this.confirmacao && confirm("Confirmar operação?")) this.$emit('botaoAtivado');
                else this.$emit('botaoAtivado');
            }
        },
        computed: {
            estiloDoBotao() {
                if(this.estilo && this.estilo == 'perigo') return "botao-perigo"
                return "botao-padrao"
            }
        }
    }

</script>

<style scoped>
    
    .botao {
        display: inline-block;
        padding: 10px;
        border-radius: 3px;
        margin: 10px;
        font-size: 1.2em;
        color: white;
    }

    .botao-perigo {
        background: firebrick;
    }

    .botao-padrao {
        background: darkcyan;
    }

</style>
