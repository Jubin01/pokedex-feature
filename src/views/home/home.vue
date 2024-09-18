<template>
  <div class="home">
    <h3>Home</h3>

    <div class="center">
      <img v-if="pokemon.sprites" id="pokeimage" :src=pokemon.sprites.front_default height="100" />
      <!-- <h5>{{ value.name.charAt(0).toUpperCase() + value.name.slice(1) }}</h5> -->
      <div>
        <h5>{{ pokemon.name }}</h5>
      </div>
      <span class="badge" v-for="(value, index) in pokemon.types" :key="index">{{ value.type.name }}</span>
      <br />
      <a v-on:click="onPrevClick" href="#" class="previous">&laquo; Previous</a>
      <a v-on:click="onNextClick" href="#" class="next">Next &raquo;</a>
    </div>

  </div>
</template>
  
<style>
a {
  padding: 8px 16px;
}

.badge {
  background-color: red;
  color: white;
  padding: 4px 8px;
  text-align: center;
  border-radius: 5px;
  margin: 0px 2px 0px 2px;
}

.center {
  text-align: center
}
</style>
<script>
export default {
  name: 'Home',
  data: () => ({
    i: 1,
    pokemon: {}
  }),
  methods: {
    onPrevClick() {
      if (this.i > 1) {
        this.callPokemon(this.i -= 1);
      }
    },
    onNextClick() {
      this.callPokemon(this.i += 1);
    },
    callPokemon(i) {
      const xhr = new XMLHttpRequest();
      xhr.open('GET', 'https://pokeapi.co/api/v2/pokemon/' + i + '/');
      xhr.onload = () => {
        this.pokemon = {};
        this.pokemon = JSON.parse(xhr.responseText);
        // document.getElementById("pokeimage").src = this.pokemon.sprites.front_default;
      }
      xhr.send();
    }
  },
  created() {
    this.callPokemon(1);
  }
};
</script>