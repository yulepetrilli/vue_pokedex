<template>
  <div class="body">
    <div class="container">
      <div class="row justify-content-center" >
        <div class="d-flex flex-column my-3" style="max-width:450px">
          <div class="text-center text-white"><h1>Pokedex</h1></div>
          <div class="my-3">
            <input 
              class="form-control" 
              type="text" 
              placeholder="Type pokemon name or ID"
              v-model="pokemonId"
              @keyup.enter="fetchData"
            >
          </div>
          <div class="text-center">
            <button 
              type="submit" 
              class="btn btn-success" 
              style="max-width:150px"
              @click="fetchData"
            >
              Search Pokemon
            </button>
          </div>
        </div>
      </div>
      <div 
        class="row justify-content-center h-100 mt-3" 
        v-if="Object.entries(pokemonData).length > 0" 
      >
        <div 
          class="card px-0" 
          style="width: 500px; height:400px;"
          
        >
          <div class="card-header text-center" >
            <h4>{{pokemonData.id}}. {{capitalize(pokemonData.name)}}</h4>
          </div>
          <img 
            :src="pokemonData.sprites.front_default" 
            :alt="pokemonData.name"
          />  
          <ul class="list-group list-group-flush">
            <li class="list-group-item">
              <ul class="list-group list-group-horizontal" id="types-list">
                <h6>Types</h6>
                <li
                  v-for="(type, index) in pokemonData.types"
                  :key="index"
                  :class="type.type.name"
                  id="type-item"
                >
                  {{type.type.name.toUpperCase()}}
                </li>
              </ul>
            </li>
            <li 
              class="list-group-item"
              v-for="(stat, index) in pokemonData.stats"
              :key="index"
              id="stats-item"
            >
              <span>{{stat.stat.name}}</span> &#8594 {{stat.base_stat}} 
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';

  export default {
    name: 'App',
    data(){
      return {
        pokemonData: {},
        pokemonId: '',
      }
    },
    methods: {
      fetchData(){
        let url = `https://pokeapi.co/api/v2/pokemon/${this.pokemonId}`;
        axios.get(url).then((res) => {
          this.pokemonData = res.data;
          console.log(res.data)
        }).catch(e => {
          return alert('Pokemon Not Found, please try again.')
        }); 
      },
      capitalize(txt){
        return txt.charAt(0).toUpperCase() + txt.slice(1);;
      },
      mounted(){
        this.fetchData();
      }
    },
  }
</script>

<style lang="scss">
  @import './pokemonTypes.scss';

  .body {
    width: 100vw;
    height: 100vh;
    background-attachment: fixed;
    background-position: center;
    background-repeat: repeat;
    background-color: #fafafa;
    background: url('./pattern.png');
  }

  img {
    height: 12rem;
    width: 12rem;
    display: block;
    margin-left: auto;
    margin-right: auto;
  }

  h6{
    padding-top: 10px;
  }

  #types-list{
    list-style-type: none;
  }

  #type-item{
    margin-left: 10px;
    padding: 5px;
    border-radius: 5px;
    color: #fff;
    font-weight: 700;
  }

  #stats-item{
    text-transform: uppercase;
  }

  span{
    font-weight: 500;
  }

  .normal {
    background-color: $normal
  }
  .fire {
    background-color: $fire
  }
  .water {
    background-color: $water
  }
  .grass {
    background-color: $grass
  }
  .electric {
    background-color: $electric
  }
  .ice {
    background-color: $ice
  }
  .fighting {
    background-color: $fighting
  }
  .poison {
    background-color: $poison
  }
  .ground {
    background-color: $ground
  }
  .flying {
    background-color: $flying
  }
  .psychic {
    background-color: $psychic
  }
  .bug {
    background-color: $bug
  }
  .rock {
    background-color: $rock
  }
  .ghost {
    background-color: $ghost
  }
  .dark {
    background-color: $dark
  }
  .dragon {
    background-color: $dragon
  }
  .steel {
    background-color: $steel
  }
  .fairy {
    background-color: $fairy
  }
</style>