<template>
  <div id="app">
    <img alt="PeakU logo" src="./assets/logo.png">
    <NavigationBar/>
    <SideBar :expanded="sideBarExpanded" @update:expanded="sideBarExpanded = $event" />
    <SearchBar :expanded="sideBarExpanded" :sticky="isStickyBar" />
    <JobList :expanded="sideBarExpanded" />
  </div>
</template>

<script>
import JobList from './components/JobList.vue'
import NavigationBar from './components/NavigationBar.vue'
import SearchBar from './components/SearchBar.vue'
import SideBar from './components/SideBar.vue'

export default {
  name: 'App',
  components: {
    JobList,
    NavigationBar,
    SearchBar,
    SideBar
  },
  data() {
    return {
      sideBarExpanded: false,
      isStickyBar: false,
    }
  },
  mounted() {
    window.addEventListener("scroll", this.handleScroll);
  },
  beforeDestroy() {
    window.removeEventListener("scroll", this.handleScroll);
  },
  methods: {
    handleScroll() {
      this.isStickyBar = window.scrollY > 70;
    },
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
