<template>
  <div class="Extension">
    <h1 class="Extension-title">
      Vocal command extension
    </h1>
    <button v-if="!listening" @click="startListening" class="Extension-button">Start talking</button>
    <div v-else class="Extension-listener">
      <div class="lds-ripple"><div></div><div></div></div>
       <button @click="stopListening" class="Extension-button">Stop talking</button>
    </div>
  </div>  
</template>

<script>
const browser = require("webextension-polyfill");

export default {
  data() {
    return {
      listening: false,
      text: "Start talking"
    };
  },
  methods: {
    startListening(){
      this.listening = true
    },
    stopListening(){
      this.listening = false
    }
  }
};
</script>

<style lang="scss" scoped>
$mainColor: #35495e;
$secondaryColor: #3ea37b;
.Extension {
  text-align: center;
  
  &-title {
    color: $mainColor;
    text-transform: uppercase;
    font-size: 20px;
    width: 200px;
  }
  &-button {
    padding: 0 20px;
    margin: 10px;
    color: $mainColor;
    background-color: $secondaryColor;
    line-height: 50px;
    transition: all linear 0.2s;
    border: none;
    border-radius: 10px;
    cursor: pointer;
    text-transform: uppercase;
    font-size: 15px;
    font-weight: 800;

    &:hover {
      box-shadow: 0px 15px 21px -11px rgba(0,0,0,0.38);
    }
  }
  &-listener {
    display: flex;
    flex-direction: column;
    align-items: center;

    .lds-ripple {
      display: inline-block;
      position: relative;
      width: 80px;
      height: 80px;

      div {
        position: absolute;
        border: 4px solid $secondaryColor;
        opacity: 1;
        border-radius: 50%;
        animation: lds-ripple 1s cubic-bezier(0, 0.2, 0.8, 1) infinite;
            &:nth-child(2) {
                animation-delay: -0.5s;
            }
        }
    }
    @keyframes lds-ripple {
      0% {
        top: 36px;
        left: 36px;
        width: 0;
        height: 0;
        opacity: 1;
      }
      100% {
        top: 0px;
        left: 0px;
        width: 72px;
        height: 72px;
        opacity: 0;
      }
    }
  }
}

</style>