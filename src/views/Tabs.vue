<template>
  <ion-page class="page">
    <div class="controls">
      <div><img src="../assets/images/logo.png" class="logo" /></div>
    <ion-grid>
  <ion-row>
    <ion-col>
        <SuperNovaCounter v-on:changed="superNovaCountChanged" :parent-count="superNovaCount" />
    </ion-col>
    <ion-col>
      <ShipCounter v-on:changed="shipCountChanged" :parent-count="shipCount" />
    </ion-col>
  </ion-row>
</ion-grid>
    </div>
  </ion-page>
<transition name="fade">
  <div class="dark-overlay" v-if="resultLose || resultWin"></div>
</transition>
<transition name="pop">
  <div class="win-loss-result" v-show="resultWin" >
      <img src="../assets/images/you-win.png"/>
      <ion-grid>
        <ion-row>
          <ion-column class="center">
            <div class="center">Play Again?</div>
            <button @click="resetGame">Yes</button>
            <span> - </span>
            <button @click="resultWin = resultLose = false">No</button>
          </ion-column>
        </ion-row>
      </ion-grid>
    </div>
</transition>

<transition name="pop">
    <div class="win-loss-result" v-show="resultLose" >
      <img src="../assets/images/you-lost.png"/>
      <ion-grid>
        <ion-row>
          <ion-column class="center">
            <div>Play Again?</div>
            <br />
            <button @click="resetGame">Yes</button>
            <span> - </span>
            <button @click="resultWin = resultLose = false">No</button>
          </ion-column>
        </ion-row>
      </ion-grid>
    </div>
</transition>
</template>

      
<style scoped>
.page
{
  text-align: center;
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-60%);
}

.controls
{
  width:400px;
  transform: scale(2,2);
  margin: 0 auto;
}
.center
{
  margin: 0 auto;
  text-align: center;
}
.logo
{
  width:40%;
  height: 40%;
  margin-bottom: 20px;
}

.win-loss-result
{
  position:absolute;
  left:0;
  top:0;
  padding: 50px;
  transform: translateY(40%) scale(1,1);
}

.dark-overlay
{
  background-color: black;
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  opacity: .85;
}

.fade-enter-active, .fade-leave-active {
    transition: opacity .5s;
    opacity: .85;
}
.fade-enter-from, .fade-leave-to {
    opacity: 0
}

.pop-enter-active, .pop-leave-active {
    transition: transform .5s;
    transform: translateY(40%) scale(1,1);
}
.pop-enter-from, .pop-leave-to {
    transform: translateY(40%) scale(0,0);
}
</style>

<script lang="ts">
import { IonPage } from '@ionic/vue';
import { ellipse, square, triangle } from 'ionicons/icons';
import SuperNovaCounter from '@/components/SuperNovaCounter.vue';
import ShipCounter from '@/components/ShipCounter.vue';

let vue: any;

export default {
  name: 'Tabs',
  components: { IonPage, SuperNovaCounter, ShipCounter },
  data() {
    return {
      superNovaCount: 0,
      shipCount: 25,
      resultWin: false,
      resultLose: false
    }
  },
  mounted()
  {
    vue = this;
    
    function resize()
    {
      const controls = document.querySelector('.controls') as HTMLDivElement;
      
      const controlsWidth = 400;
      const controlsHeight = 500;
      const scale = Math.min(
        window.innerWidth / controlsWidth,    
        window.innerHeight / controlsHeight
      );
      controls.style.transform = `scale(${scale})`;
    }
    window.onresize = resize;
    (this as any).$nextTick(function () {
      resize();
    })
    
  },
  setup() {
    return {
      SuperNovaCounter,
      ShipCounter,
      ellipse, 
      square, 
      triangle,
    }
  },
  methods: {
    superNovaCountChanged(value: number)
    {
      vue.superNovaCount += value;
      if(vue.superNovaCount < 0) vue.superNovaCount = 0;

      if(vue.superNovaCount >= 1500 || vue.superNovaCount > vue.shipCount)
      {
        vue.resultLose = true;
      }
    },
    shipCountChanged(value: number)
    {
      vue.shipCount += value;
      if(vue.shipCount < 25) vue.shipCount = 25;

      if(vue.shipCount >= 1525)
      {
        vue.resultWin = true;
      }
    },
    resetGame()
    {
      vue.superNovaCount = 0;
      vue.shipCount = 25;
      vue.resultLose = vue.resultWin = false;
    }
  }
}
</script>