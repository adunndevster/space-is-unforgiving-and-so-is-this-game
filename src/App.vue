<template>
  <ion-app>
    <ion-router-outlet />
  </ion-app>
</template>

<style>

@font-face {   
  font-family: 'Roboto Mono Thin';
  src: url('./assets/fonts/RobotoMono-Thin.ttf');
}

*{
  font-size: 24px;
}

body
{
  background-image: url("./assets/images/bg.png") !important;
  background-repeat: no-repeat !important;
  background-size: cover !important;
  color: white!important;
}

.title
{
  margin: 0px 0px 20px 0px;
  font-size: 30px;
}
.title img{
  max-height: 16px;
}

.counter
{
  font-size: 46px;
  letter-spacing: 10px;
  font-family:'Roboto Mono Thin' !important;
  color: #ff916b;
  text-shadow: 2px 2px 150px #ff916b;
  background-image: url("./assets/images/nixie-tube.png") !important;
  background-repeat: no-repeat !important;
  background-position: center;
  background-size: 150px 100px !important;
  width:170px;
  height: 100px;
  text-align: right;
  padding: 21px 3px 0px 0px;
}

</style>

<script lang="ts">
import { IonApp, IonRouterOutlet } from '@ionic/vue';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'App',
  components: {
    IonApp,
    IonRouterOutlet
  }
});
</script>