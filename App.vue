//単一ファイルコンポーネント

<template>
  <div>
    <LikeHeader>
      <h2>みなさん</h2>
      <template v-slot:title="slotProps">
        <h2>こんにちは</h2>
        <h2>{{ slotProps.user.firstName }}</h2>
      </template>
      <h3>はじめまして</h3>
      <p>よろしくお願いします</p>
      <template v-slot:number>
        <p>{{ number }}</p>
      </template>
    </LikeHeader>
    <LikeNumber :total-number="number" @my-click="incrementNumber"></LikeNumber>
    <LikeNumber :total-number="number"></LikeNumber>
    <button @click="currentComponent = 'Home'">Home</button>
    <button @click="currentComponent = 'About'">About</button>
    <Home v-if="currentComponent === 'Home'"></Home>
    <About v-if="currentComponent === 'About'"></About>
    <keep-alive>
      <component :is="currentComponent"></component>
    </keep-alive>
  </div>
</template>

<script>
  import LikeHeader from './components/LikeHeader.vue'
  import About from './components/About.vue'
  import Home from './components/Home.vue'

  export default {
    data() {
      return {
        number: 14,
        currentComponent: Home,
      }
    },
    components: {
      LikeHeader,
      About,
      Home,
    },
    methods: {
      //ここでのvalueはLikeNumber.vueの$emitの第二引数であるデータが入ってくる
      incrementNumber(value) {
        this.number = value;
      }
    },
  }
</script>

<style scoped>
  div {
  border: 1px solid blue;
  }
</style>
