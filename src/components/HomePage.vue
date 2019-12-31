<!-- TODO ajouter le nombre de nuits, bien lancer la requete vers l'API, afficher les résultats sur un autre Element (resultsSearch.Vue) -->
<template>
  <div>
   <div class="mt-5 text-4xl font-bold font-bold">Cheap-Flight</div>

          <div class="search-bar block">
               <div class="container sm:mt-2 md:mt-10 ">
                       <div class=" w-full mb-10 flex flex-col md:flex-row justify-around ">
                           <div class="w-full md:w-1/4">
                            <label for="fly_from">Départ de:  </label>
                           </div>
                           <div class="ml-0 md:ml-2 w-full md:w-3/4">
                            <input  class="w-full"  v-model="userData.fly_from" id="fly_from" type="text">
                           </div>
                       </div>
                   <div class="w-full flex flex-wrap justify-center">

                       <div class="w-1/2 flex flex-col md:flex-row ">
                               <div>
                                   <label for="price">price</label>
                               </div>
                               <div class="ml-0 md:ml-2">
                                   <input id="price" type="number" v-model.number="userData.price">&nbsp;€
                               </div>
                           </div>
                       <div class="flex flex-col md:flex-row justify-center align-middle">
                           <div>
                               <label for="nb_travelers">Voyageurs : </label>
                           </div>
                           <div class="ml-0 md:ml-2">
                               <input id="nb_travelers" v-model.number="userData.adults" type="number">
                           </div>
                       </div>
                   </div>
                   <div class="w-full flex flex-wrap justify-center my-5">

                       <div class="w-1/2 flex flex-col md:flex-row ">
                           <div>
                               <label for="price">Date de départ</label>
                           </div>
                           <div class="ml-0 md:ml-2">
                               <input id="date_from" type="date" v-model="userData.date_from">
                           </div>
                       </div>
                       <div class="flex flex-col md:flex-row justify-center align-middle">
                           <div>
                               <label for="nights_in_dest_from">Jours </label>
                           </div>
                           <div class="ml-0 md:ml-2">
                               <input id="nights_in_dest_from" v-model.number="userData.nights_in_dest_from" type="number">
                           </div>
                       </div>
                   </div>
               </div>
               <div class="mt-10"></div>
               <div class="text-left mb-5 ">Régions préférées</div>
               <div class="destinations-choices container  flex flex-wrap mb-10">
                <div class="flex flex-col md:flex-row w-full align-middle justify-around">
                    <div>
                        <label for="eu">Europe</label>
                    </div>
                    <div class="ml-0 md:ml-2">
                        <input id="eu" value="Europe" type="checkbox" v-model="userData.regions">
                    </div>
                    <div>
                        <label for="na">Amerique du Nord</label>
                    </div>
                    <div class="ml-0 md:ml-2">
                        <input id="na" value="NA" type="checkbox" v-model="userData.regions">
                    </div>
                    <div>
                        <label for="sa">Amerique du Sud</label>
                    </div>
                    <div class="ml-0 md:ml-2">
                        <input id="sa" value="LAT" type="checkbox" v-model="userData.regions">
                    </div>
                    <div>
                    <label for="as">Asia</label>
                </div>
                    <div class="ml-0 md:ml-2">
                        <input id="as" value="AS" type="checkbox" v-model="userData.regions">
                    </div>
                </div>
            </div>
               <button type="submit" v-on:click="checkForm()" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">Search</button>
           </div>
  </div>
</template>

<script>
  const axios = require("axios");
  const queryString = require('query-string');
  const moment = require('moment');

  export default {
  name: 'HomePage',
    data(){
      return {
          userData : {
              regions: [],
              adults: 0,
              price: 0,
              fly_from: '',
              nights_in_dest_from : 1,
              date_from : "",
          }
      }
    },
    computed: {
    },
    methods: {
      checkForm: function () {
          let date = moment(this.userData.date_from);
          this.userData.date_from = date.format("DD/MM/YYYY");
          let query =  queryString.stringify(this.userData);
          axios.get('http://localhost:8000/search?'+ query).then(function (result)
          {
            console.log('here');
            console.log(result);
          })
      },

    }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import '../assets/css/homepage.css';
</style>
