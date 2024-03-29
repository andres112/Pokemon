<template>
  <div class="battle">
    <b-row class="d-block d-md-none ">
      <div class="img_button">
        <!-- disable button when pokemons retrieving is loading -->
        <button class="img_button" @click.prevent="getDetails" :disabled="load">
          <img class="img-responsive" src="@/assets/pokeball.png" />
        </button>
      </div>
    </b-row>
    <!-- Spinner for loading waiting -->
    <sync-loader
      :loading="load"
      :color="'#fd3d30'"
      class="justify-content-center my-2"
    ></sync-loader>
    <b-row class=" justify-content-between" v-if="players.length > 0">
      <b-col cols="12" md="5">
        <h3 v-bind:style="[{ color: players[0].color }]">
          {{ players[0].name }} - {{ checkgender(players[0].gender) }}
        </h3>
        <table class="table table-sm table-striped table-dark table-hover ">
          <thead>
            <tr>
              <th scope="col"></th>
              <th scope="col">Name</th>
              <th scope="col">St.</th>
              <th scope="col" class="d-none d-sm-block">Avatar</th>
            </tr>
          </thead>
          <tbody v-show="!load">
            <tr
              v-for="pokemon of players[0].pokemonList"
              v-bind:key="pokemon.name"
            >
              <td class="text-center align-middle">
                <div @click="selectPokemon(pokemon)">
                  <p-radio
                    class="p-icon p-round p-tada ml-2"
                    name="Player1_Pokemon"
                    color="success"
                    :checked="pokemon.isSelected"
                  >
                    <i slot="extra" class="icon fa fa-check"></i>
                  </p-radio>
                </div>
              </td>
              <td
                class="text-center align-middle"
                @click="pokemonDetails(pokemon.name)"
              >
                {{ pokemon.name }}
              </td>
              <td
                class="text-center align-middle"
                @click="pokemonDetails(pokemon.name)"
              >
                <span class="badge badge-danger badge-pill">{{
                  pokemon.stats.find((x) => x.name == "attack").value
                }}</span>
                <span class="badge badge-success badge-pill ml-1">{{
                  pokemon.stats.find((x) => x.name == "defense").value
                }}</span>
              </td>
              <!-- This class="d-none d-md-block" hide the image and column for image when screen is smaller than md -->
              <td
                @click="pokemonDetails(pokemon.name)"
                class="d-none d-sm-block"
              >
                <img
                  :src="checkImage(pokemon.photo)"
                  :alt="pokemon.name"
                  class="img-responsive"
                  height="auto"
                  width="75"
                />
              </td>
            </tr>
          </tbody>
        </table>
      </b-col>
      <b-col cols="2" class="d-none d-md-block">
        <button class="img_button" @click.prevent="getDetails" :disabled="load">
          <img class="img-responsive" src="@/assets/pokeball.png" />
        </button>
      </b-col>
      <b-col cols="12" md="5">
        <h3 v-bind:style="[{ color: players[1].color }]">
          {{ players[1].name }} - {{ checkgender(players[1].gender) }}
        </h3>
        <table class="table table-sm table-striped table-dark table-hover">
          <thead>
            <tr>
              <th scope="col"></th>
              <th scope="col">Name</th>
              <th scope="col">St</th>
              <th scope="col" class="d-none d-sm-block">Avatar</th>
            </tr>
          </thead>
          <tbody v-show="!load">
            <tr
              v-for="pokemon in players[1].pokemonList"
              v-bind:key="pokemon.name"
            >
              <td class="text-center align-middle">
                <div @click="selectPokemon(pokemon)">
                  <p-radio
                    class="p-icon p-round p-tada ml-2"
                    name="Player2_Pokemon"
                    color="success"
                    :checked="pokemon.isSelected"
                  >
                    <i slot="extra" class="icon fa fa-check"></i>
                  </p-radio>
                </div>
              </td>
              <td
                class="text-center align-middle"
                @click="pokemonDetails(pokemon.name)"
              >
                {{ pokemon.name }}
              </td>
              <td
                class="text-center align-middle"
                @click="pokemonDetails(pokemon.name)"
              >
                <span class="badge badge-danger badge-pill">{{
                  pokemon.stats.find((x) => x.name == "attack").value
                }}</span>
                <span class="badge badge-success badge-pill ml-1">{{
                  pokemon.stats.find((x) => x.name == "defense").value
                }}</span>
              </td>
              <td
                @click="pokemonDetails(pokemon.name)"
                class="d-none d-sm-block"
              >
                <img
                  :src="checkImage(pokemon.photo)"
                  :alt="pokemon.name"
                  class="img-responsive"
                  height="auto"
                  width="75"
                />
              </td>
            </tr>
          </tbody>
        </table>
      </b-col>
    </b-row>
  </div>
</template>

<script>
import { mapState, mapActions, mapMutations } from "vuex"
import support from "@/assets/scripts/functions.js"
import router from "@/router"

//Spinner library
import Loader from "vue-spinner/src/SyncLoader.vue"

export default {
  name: "Battle",
  components: {
    "sync-loader": Loader,
  },
  computed: {
    ...mapState({
      players: (state) => state.battle.players,
      load: (state) => state.pokemon.load
    }),
  },
  methods: {
    ...mapMutations({ selectPokemon: "battle/selectPokemon" }),
    ...mapActions({
      getPokemons: "pokemon/getPokemons",
      getDetails: "pokemon/getDetails"
    }),

    // Particular functions to this component
    checkImage(image) {
      return support.checkImage(image)
    },
    checkgender(gender) {
      return support.checkgender(gender)
    },
    pokemonDetails(name) {
      // push the dynamic route to the router, trigger a route
      // this.$router.push({ name: "Pokemon", params: { id: name } });
      router.push({ name: "Pokemon", params: { id: name } })
    },
  },
  created() {
    // this allows to dispatch an action just when DOM is loaded
    this.getPokemons()
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  margin-top: 20px;
}
td {
  cursor: pointer;
}
.img_button {
  border: none !important;
  background: transparent;
  outline: none;
}
.img_button img {
  -webkit-transform: rotate(30deg) scale(0.5);
  transform: rotate(30deg) scale(0.5);
  -webkit-transition: 0.3s ease-in-out;
  transition: 0.3s ease-in-out;
  width: 75%;
  max-width: 100px;
  height: auto;
  cursor: pointer;
}
.img_button img:active {
  /*on Click*/
  -ms-transform: translateY(10px);
  -webkit-transform: translateY(10px);
  transform: translateY(10px); /*Move down*/
}
.table {
  margin-top: 10px;
}
.table td {
  padding-top: 0;
  padding-bottom: 0;
  font-family: "Baloo Da 2", cursive;
}
</style>
