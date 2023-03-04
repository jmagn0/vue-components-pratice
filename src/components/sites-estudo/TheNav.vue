<template>
    <base-card>
        <base-button @click="selecionarGuia('website-list')" :mode="sitesButtonMode">Sites</base-button>
        <base-button @click="selecionarGuia('add-website')" :mode="adicionarButtonMode">Adicionar Site</base-button>
    </base-card>
    <keep-alive>
        <component :is="guiaSelecionada"></component>
    </keep-alive>
</template>

<script>
import AddWebsite from './AddWebsite.vue';
import WebsiteList from './WebsiteList.vue';

export default {
    components: {
        AddWebsite,
        WebsiteList
    },
    data(){
        return {
            guiaSelecionada: 'website-list',
            recursosEstudo: [
                {
                    id: 'vue',
                    titulo: 'Vue.JS',
                    descricao: 'Site documentação oficial do Vue.JS.',
                    link: 'https://vuejs.org'
                },
                {
                    id: 'stackoverflow',
                    titulo: 'Stack Overflow',
                    descricao: 'Site onde você nunca ve a Home Page.',
                    link: 'https://stackoverflow.com'
                },
            ],
        };
    },
    computed: {
        adicionarButtonMode(){
            return this.guiaSelecionada === 'add-website' ? null : 'flat';
        },
        sitesButtonMode(){
            return this.guiaSelecionada === 'website-list' ? null : 'flat';
        }        
    },
    provide(){
        return{
            websites: this.recursosEstudo,
            addSite: this.adicionarSite,
            deletarSite: this.removerSite
        }
    },
    methods: {
        selecionarGuia(guia){
            this.guiaSelecionada = guia;
        },
        adicionarSite(titulo, descricao, link){
            const novoSiteObj = {
                id: new Date().toISOString(), //não sei outra maneira de fazer atualmente algo único para esse obj
                titulo: titulo,
                descricao: descricao,
                link: link
            }
            this.recursosEstudo.unshift(novoSiteObj);
            this.guiaSelecionada = 'website-list';
        },
        removerSite(siteId){
            const siteIndex = this.recursosEstudo.findIndex(site => site.id === siteId);
            this.recursosEstudo.splice(siteIndex, 1);
        }
    }
}
</script>

<style scoped>
nav {
    display: flex;   
}

div {
    padding: 1rem 1.25rem;
}

.active{
    background-color: rgb(34, 34, 104);
    color: white;
}
</style>