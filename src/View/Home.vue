<script setup>
import { onMounted, reactive, ref, computed } from "vue";
import PokemonsList from "../components/PokemonsList.vue";
import CardPokemonSelected from "../components/CardPokemonSelected.vue";

let baseUrlSvg = ref(
  "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/"
);
let pokemons = reactive(ref());
let searchPokemonField = ref("");
let pokemonSelected = reactive(ref());

onMounted(() => {
  fetch("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
    .then((res) => res.json())
    .then((res) => (pokemons.value = res.results));
});

const pokemonsFiltered = computed(() => {
  if (pokemons.value && searchPokemonField.value) {
    return pokemons.value.filter((pokemon) =>
      pokemon.name
        .toLowerCase()
        .includes(searchPokemonField.value.toLowerCase())
    );
  }
  console.log(pokemons.value);
  return pokemons.value;
});

const selectPokemon = async (pokemon) => {
  await fetch(pokemon.url)
    .then((res) => res.json())
    .then((res) => (pokemonSelected.value = res));

  console.log(pokemonSelected.value.stats);
};
</script>

<template>
  <main>
    <div class="container text-body-secondary">
      <div class="row mt-4">
        <div class="col-sm-12 col-md-4">
          <label hidden for="searchPokemonField" class="form-label"
            >Pesquisar</label
          >
          <input
            v-model="searchPokemonField"
            type="text"
            class="form-control"
            id="searchPokemonField"
            placeholder="Pesquisar..."
          />

          <CardPokemonSelected
            :name="pokemonSelected?.name"
            :hp="pokemonSelected?.stats[0].base_stat"
            :attack="pokemonSelected?.stats[1].base_stat"
            :defense="pokemonSelected?.stats[2].base_stat"
            :specialattack="pokemonSelected?.stats[3].base_stat"
            :specialdefense="pokemonSelected?.stats[4].base_stat"
            :speed="pokemonSelected?.stats[5].base_stat"
            :image="pokemonSelected?.sprites.other.dream_world.front_default"
          />
        </div>

        <div class="col-sm-12 col-md-8">
          <div class="card card-list">
            <div class="card-body row">
              <PokemonsList
                v-for="pokemon in pokemonsFiltered"
                :key="pokemon.name"
                :name="pokemon.name"
                :baseUrlSvg="baseUrlSvg + pokemon.url.split('/')[6] + '.svg'"
                @click="selectPokemon(pokemon)"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>
