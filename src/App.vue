<template>
  <div id="app">
    <comp-header/>
    <h1>{{ msg }}</h1>
    <input type="text" name="" id="" placeholder="nhap so hinh" v-model="keynumber" @input="getImages()">
      <comp-list
      v-bind:images="images"
      @ClickImgEvent="ClickImgEvent"/>

    <comp-footer/>
  </div>
</template>

<script>
import CompHeader from './components/CompHeader.vue'
import CompFooter from './components/CompFooter.vue'
import CompList from './components/CompList.vue'



export default {
  name: 'app',
  data () {
    return {
      msg: 'Hello to Your Vue.js App',
      images:[],
      page: 1,
      disable: false,
      pageSize: 30,
      nextItem:0,
      keynumber:''
    }
  },
  components: {
    CompHeader,
    CompFooter,
    CompList,

  },
// created () {
//     this.getImages(6);
//     window.addEventListener('scroll', this.handleScroll);
// },
// destroyed () {
//   window.removeEventListener('scroll', this.handleScroll);
// },
  methods: {
      // handleScroll() {
      //   window.addEventListener('scroll', e => {
      //     var scrollPos = window.scrollY
      //     var winHeight = window.innerHeight
      //     var docHeight = document.documentElement.scrollHeight
      //     if(scrollPos + winHeight >= docHeight) {
      //           this.loadImg()
      //       }
      //   });

      // },
      // loadImg() {
      //     this.loading = true;
      //     setTimeout(e => {
      //         for (var i = 0; i < 8; i++) {
      //             this.nextItem = this.images.length + 4;
      //             this.getImages(this.nextItem)
      //         }
      //         this.loading = false;
      //     }, 200);
      //     console.log(this.images.length)
      // },
      getImages() {
          var apiGiphy = `https://api.giphy.com/v1/gifs/trending?api_key=v6rKrvuRYH6cetg4lKfl4PdWJzXociiF&limit=${this.keynumber}`
          fetch(apiGiphy)
              .then(response => response.json())
              .then(result => {
                  this.images = result.data;
              })
      },
      ClickImgEvent(imgID){
        // console.log(imgID.id)
      },

  },



}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
input {
  margin-bottom: 30px;
  padding: 5px 10px;
  font-size: 4vw;
}


</style>
