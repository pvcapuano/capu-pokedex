<script setup>
const pokemon = defineProps([
  "name",
  "hp",
  "attack",
  "defense",
  "specialattack",
  "specialdefense",
  "speed",
  "image",
]);
</script>

<template>
  <div
    class="card CardPokemonSelected"
    :class="loading ? '' : 'animate__animated animate__flipInY'"
  >
    <img
      v-if="pokemon.name"
      :src="pokemon.image"
      class="card-img-top pt-2"
      :alt="pokemon.name"
      height="150"
    />
    <img
      v-else
      src="../assets/vue.svg"
      class="card-img-top pt-2"
      alt="???"
      height="150"
    />

    <div class="card-body">
      <h5 class="card-title text-center">{{ pokemon.name }}</h5>
      <hr />
      <div class="row">
        <section class="col">
          <strong>HP: </strong>
          <span>{{ pokemon.hp }}</span>
        </section>
        <section>
          <strong>Attack: </strong>
          <span>{{ pokemon.attack }}</span>
        </section>
        <section>
          <strong>Defense: </strong>
          <span>{{ pokemon.defense }}</span>
        </section>

        <section class="col">
          <strong>Special Attack: </strong>
          <span>{{ pokemon.specialattack }}</span>
        </section>
        <section>
          <strong>Special Defense: </strong>
          <span>{{ pokemon.specialdefense }}</span>
        </section>
        <section>
          <strong>Speed: </strong>
          <span>{{ pokemon.speed }}</span>
        </section>
      </div>
    </div>
  </div>
</template>
