<template>
    <div id="slider" :style="achtergrondSlider">

      <div class="fotos" :style="fotosDiv">
            <div class="pijlLinks" :class="fotoNummer === 0 ? 'onzichtbaar': ''" @click="pijlLinks"></div>

                  <slides :images="images[fotoNummer]" 
                  :slideImageBreedte="slideImageBreedte" 
                  :slideImageHoogte="slideImageHoogte"
                  :slidesBreedte="slidesBreedte"
                  :slidesHoogte="slidesHoogte"></slides>

            <div class="pijlRechts" :class="fotoNummer === (images.length - 1) ? 'onzichtbaar': ''" @click="pijlRechts"></div>
      </div>

      <div class="vierkantjes">
            <div @click="rondjes(index)" class="rondjes" 
                  :class="index === fotoNummer ? 'huidigeFoto': '' " 
                  v-for="(image, index) of images" :key="index"></div>
      </div>

    </div>
</template>

<script>
import Slides from './Slides.vue'
export default {
    components: {
        Slides
    },
    data(){
        return {
            images:[
            {
                  bron: "../fotos/space1.png",
                  bijschrift: "Gaswolk in de ruimte",
            },
                  {
                  bron: "../fotos/space2.png",
                  bijschrift: "Prachtige kleuren van een gaswolk",
            },
                  {
                  bron: "../fotos/space3.png",
                  bijschrift: "De zon in een ander lichtpunt",
            },
                  {
                  bron: "../fotos/space4.png",
                  bijschrift: "Enkele wolken formaties",
            },
                  {
                  bron: "../fotos/space5.png",
                  bijschrift: "Een gekleurde sterren verzameling",
            },
                  {
                  bron: "../fotos/space6.png",
                  bijschrift: "Enkele spaceplanes van de nato :-)",
            },
                  {
                  bron: "../fotos/space7.png",
                  bijschrift: "Een futuristische kijk in de ruimte",
            },

                  ],
                  fotoNummer: 0,
                  intervalObject: null,
                  slideImageBreedte: 640,
                  slideImageHoogte: 360,
                  slidesBreedte: 660,
                  slidesHoogte: 390,
                  fotoBreedte: 660,
                  fotoHoogte: 420,
            }
      },
      props: {
            sliderWidth: {
                  type: Number,
            },
            sliderHeight: {
                  type: Number,
            },
            intervalTijd: {
                  type: Number,
            },
      },
      methods: {
          pijlLinks() {
                  clearInterval(this.intervalObject);

                  this.moveLeft();
                  this.rechtsBewegen();
          },
          pijlRechts(){
                clearInterval(this.intervalObject);

                  this.moveRight();
                  this.rechtsBewegen();
          },
            moveLeft() {
            
                  this.fotoNummer--;
            
                  if(this.fotoNummer < 0) {
                        this.fotoNummer = (this.images.length -1);
                  }
                  
          },
            moveRight() {
            
                  this.fotoNummer++;
            
                  if(this.fotoNummer >= this.images.length) {
                        this.fotoNummer = 0;
                  }

            },
            rondjes(index) {
                  this.fotoNummer = index;
                  clearInterval(this.intervalObject);
                  this.rechtsBewegen();
            },
            rechtsBewegen() {
                  this.intervalObject = setInterval(() =>{
                        this.moveRight();
                  }, this.intervalTijd);
            },
      },
      computed: {
            achtergrondSlider(){
                  return {
                        width: this.sliderWidth + "px",
                        height: this.sliderHeight + "px",
                  }

          },
            fotosDiv(){
                  return {
                        width: this.fotoBreedte + "px",
                        height: this.frotHoogte + "px",
                  }
                
          }
      },
      created(){
            this.rechtsBewegen();
      },
}
</script>

<style scoped>

#slider {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      background-color: #eee;
      margin-top: 10px;
      margin-left: 10px;
      padding-top: 10px;
}
.fotos {
      display: flex;
      justify-content: center;
      align-items: center;
      background-color: grey;
}
.pijlLinks, .pijlRechts {
      width: 5px;
      border: 15px solid transparent; 
      display: flex;
      cursor: pointer;
}
.pijlLinks {
    margin-right: 12px;
    border-right-color: grey;  
}
.pijlRechts {
      margin-left: 12px;
      border-left-color: grey;
}
.onzichtbaar {
      visibility: hidden;
}
.vierkantjes {
      cursor: pointer;
      display: flex;
      justify-content: space-between;
      margin-top: 10px;
}
.rondjes {
      border-radius: 50%;
      height: 20px;
      width: 20px;
      margin-left: 3px;
      background-color: rgb(245, 150, 9);
}
.huidigeFoto {
      background-color: yellow;
}
</style>
