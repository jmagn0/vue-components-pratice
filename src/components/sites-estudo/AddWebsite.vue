<template>
    <base-dialog v-if="isInputInvalid" titulo="Ops! Algo deu errado." @fechar="confirmarErro">
        <template #default>
            <p>É necessário preencher todos os campos!</p>
        </template>
        <template #acoes>
            <base-button @click="confirmarErro">Ok</base-button>
        </template>
    </base-dialog>
    <base-card>
        <form @submit.prevent="adicionarSite">
            <div class="controle-formulario">
                <label for="titulo">Titulo</label>
                <input type="text" name="titulo" id="titulo" ref="inputTitulo">
            </div>
            <div class="controle-formulario">
                <label for="descricao">Descrição</label>
                <textarea name="descricao" id="descricao" rows="3" ref="inputDesc"></textarea>
            </div>
            <div class="controle-formulario">
                <label for="link">Endereço do Site</label>
                <input type="url" name="link" id="link" ref="inputLink">
            </div>
            <div>
                <base-button type="submit">Adicionar Site</base-button>
            </div>
        </form>
    </base-card>
</template>

<script>
export default {
    inject: ['addSite'],
    data(){
        return { 
            isInputInvalid: false
        };        
    },
    methods: {
        // Poderia fazer com v-model também mas nunca tinha utilizado o $refs
        adicionarSite(){
            const entradaTitulo = this.$refs.inputTitulo.value;
            const entradaDesc = this.$refs.inputDesc.value;
            const entradaLink = this.$refs.inputLink.value;

            if(entradaTitulo.trim() === '' || entradaDesc.trim() === '' || entradaLink.trim() === ''){
                this.isInputInvalid = true;
                return;
            }

            this.addSite(entradaTitulo, entradaDesc, entradaLink);
        },
        confirmarErro(){
            this.isInputInvalid = false;
        }
    }
}
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.controle-formulario {
  margin: 1rem 0;
}
</style>