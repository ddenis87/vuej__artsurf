<template>
  <div class="card">
    <div class="card__index">
      <h5 class="title">{{ pIndex + 1 }}</h5>
    </div>
    <div class="card__images">
      <img class="card__images-item"
           :src="pItem.image_url"
           :alt="pItem.name" />
    </div>
    <div class="card__body">
      <div class="card__body-head">
        <h4 class="body__name">{{ pItem.name }}</h4>
        <div class="control">
          <button class="control__button control__button_change"
                  @click="$emit('item-change', pIndex)"></button>
          <button class="control__button control__button_delete"
                  @click="$emit('item-delete', pIndex)"></button>
        </div>
      </div>
      
      <p class="body__description"><b>Description:</b> {{ pItem.description }}</p>
      <p class="body__brewers-tips"><b>Brewers tips:</b> {{ pItem.brewers_tips }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'card',
  props: ['inItem', 'inIndex'],
  computed: {
    pItem() { return this.inItem; },
    pIndex() { return this.inIndex }
  }
}
</script>

<style lang="scss" scoped>
.card {
  display: flex;
  justify-content: flex-start;
  min-height: 240px;
  border-bottom: 2px solid darkgreen;
  padding: 5px 0px;
  &__index { display: flex; justify-content: center; align-self: center; min-width: 60px; }
  &__images {
    display: flex;
    justify-content: center;
    align-items: center;
    min-width: 140px;
    max-width: 140px;
    border-right: 1px solid grey;
    border-left: 1px solid grey;
    box-sizing: border-box;
    overflow: hidden;
    &-item {
      width: auto;
      height: 220px;
    }
  }
  &__body {
    width: 100%;
    align-items: flex-start;
    padding: 0px 10px;
    box-sizing: border-box;
    .body__description { text-align: justify; }
    .body__brewers-tips { text-align: justify; }

    &-head {
      display: flex;
      justify-content: space-between;
      align-items: center;

      .control__button {
        width: 30px;
        height: 30px;
        margin: 0px 10px;
        border: 0px;
        background-color: white;
        background-position: center;
        background-size: cover;
        transition: transform .5s;
        outline: none;
        cursor: pointer;
        &_change { 
          background-image: url('~@/assets/images/change.png');
        }
        &_delete { 
          background-image: url('~@/assets/images/delete.png');
        }
        &:hover {
          transform: scale(1.2);
        }
      }
    }
  }
}
</style>