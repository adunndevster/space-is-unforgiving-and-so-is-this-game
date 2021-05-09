<template>
  <div id="container">
    <div class="title"><img src="../assets/images/supernova.png" /></div>
    <button @click="plusClick">+100</button>
    <div class="counter">{{count}}</div>
    <button @click="minusClick">-100</button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent( {
  name: 'SuperNovaCounter',
  props: {
    name: String
  },
  data() {
    return {
      count: 0
    }
  },
  methods: {
    plusClick() {
      this.count += 100;
      this.$emit('changed', this.count);
    },
    minusClick() {
      if(this.count > 0) this.count -= 100;
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