<template>
    <div>

        <div class="container" id="app_contacte" >
            <div>
            <ul class="list-inline">
                <li class="list-inline-item"> <router-link to="/"> Home </router-link> </li>
            </ul>   
            </div>
            <div class="row card" >
                <div class="col-lg-8" >
                    <div class="col-lg-8 text-center">
                        <h2>Connexion </h2>
                        <h2 v-show="loggedIn" >Connected </h2>
                    </div>
                    <div class="col-lg-2"><img src="../assets/logo.png" alt="logo">
                    </div>
                    <form name="sentMessage" id="contactForm" >
                            <div class="col-md-8">
                                <div class="form-group">
                                    <input v-model="email" type="email" class="form-control" placeholder="Votre Email *" id="email" required data-validation-required-message="Merci de rentrer votre addresse email .">
                                    <p class="help-block text-danger"></p>
                                </div>
                            </div>
                            <div class="col-md-8">
                                <div class="form-group">
                                    <input v-model="password" type="password" class="form-control" 
                                        placeholder="Votre mot de passe" id="password" 
                                        required data-validation-required-message="Merci de rentrer votre password .">
                                    <p class="help-block text-danger"></p>
                                </div>
                            </div>
                            <div class="clearfix"></div>

                            <div class="col-lg-12 mb-3 form-check">
                                <div v-show="error" id="success" class="bg-info text-warning" >[[ error ]]</div>
                                <button type="submit" @click.prevent="onLogin" class="btn btn-success btn-lg">Connectez</button>
                            </div>
                            <div v-show="!showForm" class="col-lg-12 text-center">
                                <div v-show="error" id="success" class="bg-success text-warning" > <h3>[[ message ]] </h3>
                                <img class="img" src="static/images/clin_oeil_anime.jpeg" alt="" width="100" height="50"></div>
                            </div>
                    </form>
                </div>
            </div>
        </div>

    </div>
</template>

<script>
import authAPI from  "../auth";
export default ({
    name : "Login",
    data : () => ({
        message : "",
        email : null,
        password: null,
        error : false, 
        showForm : true,
        isSaved : false,
        loggedIn : false,
    }),
    methods :{
        
        onLogin(){
            authAPI.login(this.email, this.password)
            .then( () =>  {
                this.$router.push("/")
                this.error = false;
                console.log("Connected !!" + this.email + " et " + this.password)
            })
            .catch( () => {
                this.error = true;
                this.message = "Erreur de connexion !!"
                console.log("Erreur de connexion !!" + this.email + this.password)
            });
        }
    }
    
})
</script>