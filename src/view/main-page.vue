<template>
  <div class="main-page">
    <h1 class="main-page__title">List Beer</h1>
    <div class="main-page__list">
      <ul>
        <li v-for="(item, index) in listItem" :key="index">
          <item-card></item-card>
        </li>
      </ul>
    </div>
    <div class="main-page__control">
      <c-button>Show next</c-button>
    </div>
    
  </div>
</template>

<script>
import axios from 'axios';

import cButton from '@/components/elements/c-button';
import itemCard from '@/components/__item-card';

export default {
  name: 'mainPage',
  components: {
    cButton,
    itemCard,
  },
  data() {
    return {
      listItem: [],
    }
  },
  created() {
    this.getList({socket: 'https://api.punkapi.com/v2/beers?page=1&limit=25'});
  },
  methods: {
    getList(objOption) {
      axios
        .get(objOption.socket, null, null)
        .then((response) => {
          for(let i = 0; i < response.data.length; i++) {
            this.listItem.push({
              name: response.data[i].name,
              img: response.data[i].img,
              description: response.data[i].description,
              brewers_tips: response.data[i].brewers_tips
            })
          }
          
           
        })
        return;
    }
  }
}
</script>

<style scoped lang="scss">
.main-page {
  max-width: 1024px;
  width: 100%;
  margin-left: auto;
  margin-right: auto;
}
</style>
