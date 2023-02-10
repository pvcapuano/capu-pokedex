<script setup>
const pokemon = defineProps(["name", "baseUrlSvg"]);
</script>

<template>
  <div class="col-4">
    <div class="card p-2 mb-3 cardListPokemon">
      <p class="text-center font-size:10vw">{{ pokemon.name }}</p>
      <img
        :src="baseUrlSvg"
        class="card-img-top mb-2"
        alt="Pokemon"
        height="90"
      />
      <a href="#" class="btn btn-primary btn-sm mb-1">Detalhes</a>
    </div>
  </div>
</template>

<style scoped>
.cardListPokemon {
  background: #e8e8e8;
  cursor: pointer;
}

.cardListPokemon:hover {
  background: #d5d1d1;
}

.cardListPokemon img:hover {
  transition: 0.3s;
  padding: 0.2rem;
}
</style>
