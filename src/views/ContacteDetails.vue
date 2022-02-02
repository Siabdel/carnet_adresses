<template>
  <div>
    <div class="container" >
        <h2> Details du contacte {{ $route.params.contacte.nom }}  </h2>
        <div>
            <img class="img-rounded" src="../assets/avatar.jpg" alt="">
        </div>
        <div class="breadcrumb">
            <p>
                {{ $route.params.contacte.titre }} 
            </p>    
            <p>
            Nom : {{ $route.params.contacte.nom }} {{ $route.params.contacte.prenom }} 
            </p>
            <p>
            Email : {{ $route.params.contacte.email }}
            </p>
            <p>
                Telephone : {{ $route.params.contacte.telephone }} 
            </p>

        </div>
    </div>
  </div>
</template>

<script>

import 'bootstrap3/dist/css/bootstrap.min.css';
export default ({
    name : "UserDetails",

    data() {
      return {
        message : "",
      }
    },

    methods: {

    }

})

</script>