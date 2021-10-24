<template>
  <div id="app">

  <ul class="flex-container">
      <li v-for="item in items.results" :key="item.id" class="flex-item">
        <div>{{ (item.pub_date) }} </div>
        <div><img :src="item.image && item.image.file" /></div>
        <div> {{ item.title }}</div>
        <div class="downloads">
          <span
            v-for="downloadable in item.downloadable.filter(
              (d) => !!d.document_en
            )"
            :key="downloadable.id"
          >
            <a :href="downloadable.document_en.file">Explore More</a>
          </span>
        </div>
      </li>
    </ul>


      
        
      
  
  </div>

</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      items:[]
    }
  },


  created() {
    axios.get(`https://zbeta2.mykuwaitnet.net/backend/en/api/v2/media-center/press-release/?page_size=61&type=5`)


    .then(response => {
     
      this.items = response.data
    })
    
  }
}

</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
ul.flex-container {
  padding: 0;
  margin: 0;
  list-style-type: none;
  display: flex;
  flex-direction: row wrap;
  flex-wrap: wrap;
  justify-content: space-around;
}
li img {
  display: initial;
  height: 100px;
}
.flex-item {
  background:aquamarine;
  width: calc(100% / 5.5);
  padding: 5px;
  height: auto;
  margin-top: 10px;
  color:black;
  font-weight: bold;
  text-align: center;
}
.downloads {
  margin-top: 10px;
}
</style>