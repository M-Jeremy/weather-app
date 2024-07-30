<script setup>
defineProps({
  msg: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="greetings">
    <h1 class='text-indigo-600' style="text-align: center;">{{ msg }}</h1>
    <h3 style="text-align: center;"> Si vous êtes ici pour la <span class='text-indigo-600'>météo</span>, alors vous êtes au bon endroit ! </h3>
    <br>
    <h3 style="text-align: center;">Faites votre recherche -></h3>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
