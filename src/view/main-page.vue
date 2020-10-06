<template>
  <div class="main-page">
    <h1 class="main-page__title">List Beer</h1>
    <c-button @click="controlGetList" :inIsLoad="controlNextLoad">Load list beer</c-button>
    <div class="main-page__list">
      <ul class="list">
        <li class="list__item" 
            v-for="(item, index) in listItem" 
            :key="index">
          <item-card :inItem="item" 
                     :inIndex="index"
                     @item-delete="itemDeleteConfirm"
                     @item-change="itemChangeDialog"></item-card>
        </li>
      </ul>
    </div>
    <div class="main-page__control">
      <c-button v-show="controlNextShow" 
                :inIsLoad="controlNextLoad"
                @click="controlGetNext">{{ controlNextText }}</c-button>
    </div>
    <dialog-delete :inItem="propsItemDelete"
                   v-if="dialogDeleteShow"
                   @close="() => {dialogDeleteShow = false}"
                   @delete="itemDelete"></dialog-delete>
    <dialog-change :inItem="propsItem"
                   v-if="dialogChangeShow"
                   @close="() => {dialogChangeShow = false}"
                   @change="itemChange"></dialog-change>
    <div class="main-page__blocked-content"
         v-if="(dialogDeleteShow || dialogChangeShow)"></div>
  </div>
</template>

<script>
import axios from 'axios';

import cButton from '@/components/elements/c-button';
import itemCard from '@/components/__item-card';
import dialogDelete from '@/components/__dialog-delete'
import dialogChange from '@/components/__dialog-change'

export default {
  name: 'mainPage',
  components: {
    cButton,
    itemCard,
    dialogDelete,
    dialogChange,
  },
  data() {
    return {
      listItem: [],
      pageNumber: 1,
      pageLimit: 25,
      urlServer: 'https://api.punkapi.com/v2/beers',
      controlNextText: 'Show next',
      controlNextLoad: false,
      controlNextShow: false,
      dialogDeleteShow: false,
      dialogChangeShow: false,
      propsItemDelete: {},
      propsItem: {},
    }
  },
  methods: {
    itemChange(newName, newDescription, index) {
      if (newName) this.listItem[index].name = newName;
      if (newDescription) this.listItem[index].description = newDescription;
      this.dialogChangeShow = false;
    },
    itemChangeDialog(item) {
      this.propsItem.index = item;
      this.propsItem.name = this.listItem[item].name;
      this.propsItem.description = this.listItem[item].description;
      this.dialogChangeShow = true;
    },
    itemDelete(item) {
      this.dialogDeleteShow = false;
      this.listItem.splice(item, 1);
    },
    itemDeleteConfirm(item) {
      this.propsItemDelete.index = item;
      this.propsItemDelete.name = this.listItem[item].name;
      this.dialogDeleteShow = true;
    },
    controlGetList() {
      this.controlNextLoad = true;
      this.controlNextShow = true;
      this.listItem = [];
      let option = {
        page: this.pageNumber,
        limit: this.pageLimit,
      }
      this.getList(this.urlServer, option);
    },
    controlGetNext() {
      this.controlNextLoad = true;
      this.controlNextText = "loading"
      this.pageNumber++;
      let option = {
        page: this.pageNumber,
        limit: this.pageLimit,
      }
      this.getList(this.urlServer, option);
    },
    getList(url, option) {
      axios
        .get(this.urlServer + `?page=${option.page}&limit=${option.limit}`, null, null)
        .then((response) => {
          if (response.data.length == 0 || response.data.length < 25) { 
            this.controlNextShow = false; 
            this.controlNextLoad = false; 
            this.controlNextText = 'Show next'
          ;}
          for(let i = 0; i < response.data.length; i++) {
            this.listItem.push({
              name: response.data[i].name,
              image_url: response.data[i].image_url,
              description: response.data[i].description,
              brewers_tips: response.data[i].brewers_tips
            });
            if(i == response.data.length - 1) 
              setTimeout(() => {
                this.controlNextLoad = false; 
                this.controlNextText = 'Show next'; 
              }, 1000); // - таймер специально для того чтобы успеть увидеть загрузку на кнопке (если сервер быстро ответит)
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

  &__list {
    .list {
      padding-left: 0px;
      &__item {
        list-style: none;
      }
    }
  }
  &__blocked-content {
    position: fixed;
    left: 0px;
    top: 0px;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, .3);
  }
}
</style>
