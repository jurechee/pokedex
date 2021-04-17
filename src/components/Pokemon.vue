<template>
  <div id="pokemon">
      <div class="card">
  <div class="card-image">
    <figure >
      <img :src="currentiImg" alt="Placeholder image">
    </figure>
  </div>
  <div class="card-content">
    <div class="media">
      
      <div class="media-content">
        <p class="title is-4">{{num}} - {{nome | upper}}</p>
        <p class="subtitle is-6">{{pokemon.type}}</p>
      </div>
    </div>

    <div class="content">
      <button class=" button is-success is-normal is-fullwidth" @click="mudarSprite">Mudar Sprite</button>
    </div>
  </div>
</div>
      
  </div>
</template>

<script>
import axios from 'axios';

export default {

    created: function(){
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name; 
            //res.data.types[0].type.name; vem da API
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            this.currentiImg = this.pokemon.front;
            console.log(this.pokemon);
        })
    },

    data(){
        return {
            isFront: true,
            currentiImg: '',
            pokemon: {
                type: '',
                front: '',
                back: ''
            }
        }
    },

    props: {
        num: Number,
        nome: String,
        url: String
    },

    filters: {
        upper: function(value){
            var upperNAme = value[0].toUpperCase() + value.slice(1);
            return upperNAme;
        }
        
    },

    methods: {
       mudarSprite: function(){
         if(this.isFront){
           this.isFront = false;
           this.currentiImg = this.pokemon.back;
         }else{
           this.isFront = true;
           this.currentiImg = this.pokemon.front;
         }

       }
    }

}
</script>

<style>
    #pokemon{
        margin-top: 2%;
    }
</style>