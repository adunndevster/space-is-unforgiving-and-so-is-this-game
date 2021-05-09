<template>
  <div id="container">
    <div class="title"><img src="../assets/images/ship.png" /></div>
    <button @click="plus100sClick">+100</button><button @click="plus25sClick">+25</button>
    <div  class="counter">{{count}}</div>
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
    name: String
  },
  data() {
    return {
      count: 0
    }
  },
  methods: {
    plus100sClick() {
      this.count += 100;
      this.$emit('changed', this.count);
    },
    minus100sClick() {
      if(this.count > 0) this.count -= 100;
      this.$emit('changed', this.count);
    },
    plus25sClick() {
      this.count += 25;
      this.$emit('changed', this.count);
    },
    minus25sClick() {
      if(this.count > 0) this.count -= 25;
      this.$emit('changed', this.count);
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