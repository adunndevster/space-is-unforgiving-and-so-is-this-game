<template>
  <ion-page class="page">
    <div class="controls">
      <div><img src="../assets/images/logo.png" class="logo" /></div>
    <ion-grid>
  <ion-row>
    <ion-col>
        <SuperNovaCounter v-on:changed="superNovaCountChanged" />
    </ion-col>
    <ion-col>
      <ShipCounter v-on:changed="shipCountChanged" />
    </ion-col>
  </ion-row>
</ion-grid>
    </div>
  </ion-page>
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
.logo
{
  width:40%;
  height: 40%;
  margin-bottom: 20px;
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
      shipCount: 0
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
      vue.superNovaCount = value;

      if(vue.superNovaCount >= 1500 || vue.superNovaCount > vue.shipCount)
      {
        alert('you lose.');
      }
    },
    shipCountChanged(value: number)
    {
      vue.shipCount = value;
      if(vue.shipCount >= 1525)
      {
        alert('you win.');
      }
    }
  }
}
</script>