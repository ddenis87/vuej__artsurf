<template>
  <div class="dialog-delete">
    <div class="body">
      <img src="@/assets/images/delete.png" alt="" class="body__images">
      <p class="body__text">Are you sure you want to delete a position?<br/>It's famous <span class="body__text_bold">{{ inItem.name }}</span></p>
    </div>
    <hr>
    <div class="control">
      <button class="control__button control__button_accept"
              @click="$emit('delete', inItem.index)"></button>
      <button class="control__button control__button_cancel"
              @click="$emit('close')"></button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'dialogDelete',
  props: ['inItem'],
}
</script>

<style lang="scss" scoped>
.dialog-delete {
  position: fixed;
  padding: 10px;
  padding-top: 20px;
  top: 30%;
  left: calc(50% - 250px);
  width: 500px;
  height: 140px;
  border: 2px solid grey;
  border-radius: 5px;
  background-color: white;
  box-shadow: 1px 1px 1px black;
  box-sizing: border-box;
  
  .body {
    display: flex;
    align-items: flex-start;
    margin-bottom: 20px;
    &__images {
      width: 50px;
      margin-right: 10px;
    }
    &__text {
      margin: 0px;
      &_bold {
        font-weight: bold;
      }
    }
  }
  .control {
    display: flex;
    justify-content: space-between;
    &__button {
      width: 25px;
      height: 25px;
      margin: 0px 10px;
      border: 0px;
      background-color: white;
      background-position: center;
      background-size: cover;
      transition: transform .5s;
      outline: none;
      cursor: pointer;
      &_accept { 
        background-image: url('~@/assets/images/accept.png');
      }
      &_cancel { 
        background-image: url('~@/assets/images/cancel.png');
      }
      &:hover {
        transform: scale(1.2);
      }
    }
  }
  
}
</style>