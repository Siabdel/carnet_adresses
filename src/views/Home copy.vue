<template>
  <div class="container">
    <h3> Home </h3>

    <img alt="Vue logo" src="../assets/logo.png">
    <SearchBox @searchKey="include_contactes" />

    <CarnetAdresse :contactes="reload_contactes" :afficher="(searchBy)?true:false"/>
    
  </div>
</template>

<script>
import CarnetAdresse from "../components/CarnetAdresse.vue";
import SearchBox  from "../components/SearchBox.vue";

export default {
  name: 'UserList',
  components: {
    CarnetAdresse,
    SearchBox,
  },
  data(){
    return {
      adresses : [],
      searchBy : "",
      sortBy : "nom",
    }
  },
  created() {
      let url = `http://51.178.136.190:93/apipro/directories/`

      // ajax load
      fetch(url)
      .then(response => response.json())
      .then(json => {
        this.adresses = json;
        //console.log(" data = " + this.adresses[0].nom )
        })  
      .catch(err =>err.msg)
  },

  methods: {
    include_contactes(search){
      // expression reguliere dans vuejs
      const url = 'https://google.com/foo/bar';
      const regex = /^(https.+)\/.*$/ig;
      const matches = regex.exec(url);
      console.log( "matches = " + matches[1]) ;/* 1 = group index */

      //console.log("terms search !!! = " + search)
      this.searchBy = search.toLowerCase()
      //return this.adresses.filter(contacte => contacte.nom.includes(search))
      return this.adresses
    },

    compare(a, b) {
      if (a.nom < b.nom)
        return -1;
      if (a.nom > b.nom)
        return 1;
      return 0;
    }
  },

  computed : 
  {
    reload_contactes(){
      if(this.searchBy){
        return this.adresses.filter(contacte => contacte.nom.toLowerCase().includes(this.searchBy)).sort(this.compare)
      }else {
        return this.adresses
        .filter( a => a.nom.includes("a"))
        .sort( (a,b) => a[this.sortBy].localeCompare(b[this.sortBy]));
      }
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
