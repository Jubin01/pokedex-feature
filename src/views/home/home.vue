<template>
  <div class="home">
    <h3>Home</h3>

    <div class="center" v-for="(value, index) in pokemon" :key="index">
      <a>
        <img :src=value.sprites.other.dream_world.front_default height="100" />
      </a>
      <h5>{{ value.name.charAt(0).toUpperCase() + value.name.slice(1) }}</h5>
      <a  class= "badge" v-for="(value, index) in value.types" :key="index">{{ value.type.name}}</a>
      <br />
      <a v-on:click="onPrevClick" href="#" class="previous">&laquo; Previous</a>
      <a v-on:click="onNextClick" href="#" class="next">Next &raquo;</a>
    </div>

  </div>
</template>
  
<style>
a {
  text-decoration: none;
  display: inline-block;
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
    pokemon: []
  }),
  methods: {
    onPrevClick: function () {
      if(this.i > 1){
        this.callPokemon(this.i-=1);
      } 
    },
    onNextClick: function () {
      this.callPokemon(this.i+=1);
    },
    callPokemon: function (i) {
      const xhr = new XMLHttpRequest();
      xhr.open('GET', 'https://pokeapi.co/api/v2/pokemon/' + i + '/');
      xhr.onload = () => {
        this.pokemon = [];
        this.pokemon.push(JSON.parse(xhr.responseText));
      }
      xhr.send();
    }
  },
  created() {
    this.callPokemon(1);
  }
};
</script>