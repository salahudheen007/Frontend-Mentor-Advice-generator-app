<script>
import AdviceVue from "./components/Advice.vue";
import patterndmobile from "./assets/images/pattern-divider-mobile.svg";
import patterndesktop from "./assets/images/pattern-divider-desktop.svg";
export default {
  name: "App",
  components: {
    AdviceVue,
  },
  data(){
    return{
      pattern:''
    }
  },
  methods:{
    updateImage(){
    if (window.innerWidth> 400) {
        this.pattern=patterndesktop
      } else {
        this.pattern=patterndmobile;
      }
  }
},
mounted(){
  this.updateImage()
},
created() {
  window.addEventListener("resize", this.updateImage);
},
destroyed() {
  window.removeEventListener("resize", this.updateImage);
},
}
</script>

<template>
<advice-vue :pattern="pattern"/>
</template>

<style scoped>
</style>
