<script setup>
import HeroSection from "../components/HeroSection.vue"
import DataList from "../components/DataList.vue"
</script>



<template>
  <main>
    <HeroSection :count="count"></HeroSection>
    <DataList @changedCount="newCount($event)"></DataList>
  </main>
</template>

<style scoped>

</style>

<script>
  export default {
    data(){
      return {
        count: null,
      }
    },
    methods: {
      newCount(newCount){
        this.count = newCount
        console.log(this.count)
      }
    }
  }
</script>
