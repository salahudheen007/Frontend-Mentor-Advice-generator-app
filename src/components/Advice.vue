<template>
  <div class="card">
    <div class="card-header">
      <h5 class="card-header-heading">ADVICE # {{advice.id}}</h5>
    </div>
    <div class="card-content">
      <p>
         "{{advice.advice}}"
      </p>
    </div>
    <div class="card-footer">
      <div class="card-footer-images">
        <img class="devider" :src="pattern" alt="" />
      </div>
      <div class="card-footer-images card-footer-dice" @click="getNewAdvice">
        <img :src="dice" alt="" class="dice" />
      </div>
    </div>
  </div>
</template>

<script>
import diceImage from "../assets/images/icon-dice.svg";
import axios from "axios";
export default {
  name: "Advice",
  props: ["pattern"],
  data() {
    return {
      dice: diceImage,
      advice: {},
    };
  },
  methods: {
    getNewAdvice() {
      axios.get("https://api.adviceslip.com/advice").then((Response) => {
        this.advice=Response.data.slip;
      }).catch((error)=>{
                    console.log(error);
                });
    },
  },
  mounted(){
    this.getNewAdvice()
  }
};
</script>

<style scoped>
.card {
  min-width: 20rem;
  max-width: 35rem;
  background-color: var(--Dark_Grayish_Blue);
  border-radius: 0.8em;
}
.card-header {
  text-align: center;
  overflow: hidden;
}
.card-header-heading {
  vertical-align: middle;
  color: var(--Neon_Green);
  font-weight: 600;
  font-size: 0.7rem;
  letter-spacing: 3px;
  margin: 2.2rem auto;
}
.card-content > * {
  color: var(--Light_Cyan);
  text-align: center;
}
.card-footer {
  height: 5rem;
  position: relative;
}

.card-footer-images {
  display: flex;
  justify-content: center;
}
.devider {
  width: 80%;
  height: 1rem;
}
.card-footer-dice {
  top: 3rem;
  position: absolute;
  padding: 1.4rem;
  background-color: var(--Neon_Green);
  border-radius: 50%;
  left: 50%;
  top: 100%;
  transform: translate(-50%, -50%);
}
.card-footer-dice:hover {
  filter: drop-shadow(1px 0px 25px var(--Neon_Green));
}

@media only screen and (min-width: 376px) {
  .card-content > * {
    font-size: 28px;
    font-weight: 800;
    margin: 0 1rem;
  }
  .card-header-heading {
    font-weight: 800;
    font-size: 1rem;
    letter-spacing: 4px;
    margin: 2.5rem auto;
  }
  .card-header {
    height: 6rem;
  }
  .card-content {
  padding-bottom: 2.2rem;
}
}
@media only screen and (max-width: 375px) {
  .card-content > * {
    font-size: 25px;
    font-weight: 600;
    margin: 0 0.5rem;
  }
  .card-header-heading {
    font-weight: 600;
    font-size: 0.7rem;
    letter-spacing: 3px;
    margin: 2.2rem auto;
  }
  .card-header {
    height: 5rem;
  }
  .card-content {
  padding-bottom: 1.5rem;
}
}
</style>