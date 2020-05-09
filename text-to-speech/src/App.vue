<template>
 <div>
  <app-header />
   <div class="app-container">
      <select></select>
      <br />
      <div class="slidercontainer">
        <input class="slider" type="range" min="0.5" max="3" id="speed" />
      </div>
      <span></span>
      <br />
      <textarea cols="30" rows="10">
kablosuzkedi'nin yeni videosuna hoşgeldiniz, ben Yelda. Eveet bu dersimizde sizlerle beraber Text To Speech konusunu göreceğiz. Şimdi vakit kaybetmeden sözü Gökhan Kandemir'e bırakıyorum.</textarea
      >
      <div class="previewContainer"></div>
      <br />
      <button class="btn red" type="button">
        <span>Söyle Bakalım Şekerim!</span>
      </button>
    </div>
 </div>
</template>

<script>

import appHeader from "@/components/appHeader";

export default {
  
  name: 'App',
  components: {
    appHeader
  },
  created(){
   this.getVoices().then(voices => {
     console.log("Voices",voices);
   });
  },
  data(){
    return{
      tts : window.speechSynthesis
    };
  },
  methods: {
    getVoices() {
      let intervalID;
      return new Promise((resolve, reject) => {
        intervalID = setInterval(() => {
          if (this.tts.getVoices().length > 0) {
            resolve(this.tts.getVoices());
            clearInterval(intervalID);
          }
        }, 10);
      });
    },
}
}
</script>

