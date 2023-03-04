<template>
    <ul>
        <website-card v-for="site in websites" :key="site.id" v-bind="site"></website-card>
    </ul> 
</template>

<script>
import WebsiteCard from './WebsiteCard.vue';

export default {
    inject: ['websites'],
    components: {
        WebsiteCard
    },
}
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>