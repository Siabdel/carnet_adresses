<template>
    <div>
        <h2> Details du contacte {{ $route.params.userId.nom }}  </h2>
        <h4> {{ message}} </h4>
    </div>
</template>

<script>

export default{
    name : 'UserDetails',
    props : ['id'],
    data(){
        return {
            message : "on est au details !!"
        }
    }

}

</script>