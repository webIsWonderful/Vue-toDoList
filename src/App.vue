<template>
  <section id="to-do-app">
    <MainHeader />
    <ToDoList />
    <SideContent />
    <Footer />
  </section>
</template>

<script>
import MainHeader from './components/MainHeader.vue'
import ToDoList from './components/ToDoList.vue'
import SideContent from './components/SideContent.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'app',
  components: {
    MainHeader,
    ToDoList,
    SideContent,
    Footer
  },
  data () {
    return {
         
    }
  }
}
</script>

<style lang="scss">

html, body{
  height: 100%;
  font-size: 1rem;
}

#to-do-app {
  font-family: 'Roboto', Helvetica, Arial, sans-serif;
  font-size: 1rem;
  height: 100%;
  display: grid;
  grid-template-columns: repeat(8, 1fr);
  grid-template-rows: 80px 1fr 1fr 80px;  
}
*:focus {
  outline: none;
}

</style>
