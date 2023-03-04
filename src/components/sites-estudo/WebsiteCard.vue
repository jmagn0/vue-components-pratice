<template>
  <li>
    <base-card>
      <header>
        <h2>{{ titulo }}</h2>
        <base-button mode="flat" @click="deletarSite(id)">Delete</base-button>
      </header>

      <p>{{ descricao }}</p>
      <nav>
        <a :href="link">Ver site</a>
      </nav>
    </base-card>
  </li>
</template>

<script>
export default {
    inject:['deletarSite'],
  props: {
    id: {
      type: String,
      required: true,
    },
    titulo: {
      type: String,
      required: true,
    },
    descricao: {
      type: String,
      required: true,
    },
    link: {
      type: String,
      required: true,
      validator: function () {
        //alguma validação para checar se o link é válido
        //não sei se é necessário, mas só pra dizer que sei
        //que é possível
        return true;
      },
    },
  },
};
</script>

<style scoped>
li {
  margin: auto;
  max-width: 40rem;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h3 {
  font-size: 1.25rem;
  margin: 0.5rem 0;
}

p {
  margin: 0.5rem 0;
}

a {
  text-decoration: none;
  color: #ce5c00;
}

a:hover,
a:active {
  color: #c89300;
}
</style>
