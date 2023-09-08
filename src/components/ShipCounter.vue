<template>
  <div id="container">
    <div class="title"><img src="../assets/images/ship.png" /></div>
    <button @click="plus100sClick">+100</button><button @click="plus25sClick">+25</button>
    <div  class="counter">{{parentCount}}</div>
    <button @click="minus100sClick">-100</button><button @click="minus25sClick">-25</button>
  </div>
</template>

<style scoped>
button {
  margin: 0px 8px 0px 8px;
}
</style>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent( {
  name: 'ShipCounter',
  props: {
    parentCount: Number
  },
  methods: {
    plus100sClick() {
      this.$emit('changed', 100);
    },
    minus100sClick() {
      this.$emit('changed', -100);
    },
    plus25sClick() {
      this.$emit('changed', 25);
    },
    minus25sClick() {
      this.$emit('changed', -25);
    }
  }
  
});
</script>

<style scoped>


#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  color: #8c8c8c;
  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>