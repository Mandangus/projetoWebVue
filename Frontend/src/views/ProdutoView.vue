<template>

<div class="container shadow-lg py-4">
    <div class="row justify-content-md-center">
        <div class="col">
            <h3>{{aula.nome}}</h3>
            <ModalRemove v-if="user.isAdmin"></ModalRemove>
        </div>
    </div>
    <div  v-if="user.isAdmin" class="row justify-content-center my-2">
        <div class="col-2" >
            <div class="form-check form-switch">
                <input class="form-check-input" type="checkbox" id="flexSwitchCheckDefault" @click="mostraVideo = !mostraVideo">
                <label class="form-check-label" for="flexSwitchCheckDefault">Visualizar Video</label>
            </div>
        </div>
    </div>

    <div class="row">
        <div  v-if="comprado || mostraVideo" class="col iframe-container mx-2">
            <iframe width="560" height="315" :src="aula.cdnSrc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
        </div>
         <div v-else class="col iframe-container mx-2">
            <iframe width="560" height="315" :src="aula.prevSrc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
        </div>
    </div>


    <div class="row justify-content-center" align="center">
        <div class="col- col-lg-5">     
            <div class="card border-dark p-2 mt-4" id="descript" style="width: 25rem;">
                <h5 class="card-title">Descrição</h5>
                <p class="card-text" style="line-height: 230%;">{{aula.description}}</p>
                    <ModalDesc v-if="user.isAdmin"></ModalDesc>
            </div>
        </div>
        <div class="col- col-lg-5 ">
            <div class="card border-0" style="width: 25rem;"> 
                <div class="row mt-4">
                    <div class="col" v-if="!comprado || user.isAdmin">
                        <h3 id="preco">{{aula.price}} </h3> 
                    </div>
                    <div class="col">
                        <ModalPreco v-if="user.isAdmin"></ModalPreco>
                        <button class="btn btn-primary btn-lg" type="submit" @click="addToCart" v-else-if="!comprado" >
                            <img :src="cartIcon" width="35" />
                            Comprar
                        </button>
                    </div>
                </div>
               
            

                <div class="row mt-4">
                    <div class="col">     
                        <p>{{aula.detalhes}}</p>
                        <ModalDet v-if="user.isAdmin"></ModalDet>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>

</template>

<script>
// import usuario from "../data/usuario.js"
import ModalDesc from "@/components/modal-desc.vue"
import ModalRemove from "../components/modal-remove.vue"
import ModalPreco from "../components/modal-preco.vue"
import ModalDet from "../components/modal-det.vue"


export default{
    name: "video_card",
    computed: {
        user() {
            return this.$store.getters.userLogged
        }
    },
     data: () => {
        return {
            mostraVideo: false,
            comprado:false && usuario.login,
            aula: {
                nome: "Álgebra Linear",
                price: "R$ 120,00",
                image: require("@/assets/thumbnails/Videoaula.png"),
                description: "Aula da disciplina Cálculo I - MCA-001. Curso de Engenharia - Turma 2016 -  Univesp Universidade Virtual do Estado de São Paulo.  Professor responsável pela disciplina: Claudio Possani Professor ministrante: Claudio Possani",
                detalhes: "Nesta aula introdutória do curso, o incrível Prof. Cláudio Possani faz um panorama das ideias abordadas pela disciplina e de sua importância na formação de um engenheiro",
                cdnSrc: "https://www.youtube.com/embed/Utj5xUmUEvk",
                prevSrc: "https://www.youtube.com/embed/u6phoAngwuI"
            },
            cartIcon: require("@/assets/icones/cart.png"),
            item: {
                nome: "Álgebra Linear ",
                price: 120,
                image: require("@/assets/thumbnails/calc3.png")
            }
        };
    },
    methods: {
        addToCart() {
            this.$store.commit("addToCart", this.aula);
        }
    },
    components: { ModalDesc, ModalRemove, ModalPreco, ModalDet }
}
</script>

<style scoped>

@media (min-width: 1200px) {
    .container{
        max-width: 1200x;
    }
}

#descript {
    background-color: #F2F3F4
}

#preco{
    color: #0d6efd;
    font-size: xx-large;
    font-weight: bolder;
}

.iframe-container{
  position: relative;
  width: 100%;
  padding-bottom: 56.25%; 
  height: 0;
}
.iframe-container iframe{
  position: absolute;
  top:0;
  left: 0;
  width: 100%;
  height: 100%;
}

</style>
