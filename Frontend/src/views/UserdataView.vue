<template>

<div class="container">

    <div class="row ">
        <div class="col- col-sm- col-md-6 col-lg-6 mt-4">
            <ul class="list-group" id="datalist">
                <li class="list-group-item border-0">Nome:   <b>{{user.name}}</b> </li>
                <li class="list-group-item border-0">Email:  <b>{{user.email}}</b> </li>
                <li class="list-group-item border-0">Endereço:   <b>{{user.address}}</b> </li>
                <li class="list-group-item border-0" v-if="user.isAdmin">Administrador </li>
        
            </ul>
        </div>
        <div class="col- col-sm- col-md-6 col-lg-6 mt-4">

            <div class="col-">
                    <img class="img-fluid" id="profPic" :src="profileImage"/>
                    <div class="row">
                        <div class="col my-3">
                        <button id="changePic" type="button" class="btn  btn">Alterar foto</button>
                        </div>
                    </div>
            </div>       
        </div>

    </div>
</div>


</template>

<script>


export default{
    name: 'user_info',
    computed: {
        user() {
            return this.$store.getters.userLogged
        }
    },
  data: ()=>{
    return {
      profileImage: require('@/assets/icones/Profile_avatar_placeholder_large.png'),
    }
  }
}

</script>


<style scoped>

li{
    font-weight: 500;
    font-size:x-large;
}

b{

    font-weight: 400;
    font-size:large;
}

#profPic{
    border-radius: 50%;
    width: 280px;    
}

#changePic{
    color:black;
}

#datalist{
    text-align: left;
}

</style>