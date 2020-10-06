<template>
  <div class="dialog-change">
    <div class="body">
      <img src="@/assets/images/change.png" alt="" class="body__images">
      <div class="body-input">
        <c-input class="body-input__input"
                 :inValue="inputName"
                 v-model="newName">name</c-input>
        <c-textarea class="body-input__textarea"
                    :inValue="inputDescription"
                    v-model="newDescription">description</c-textarea>
      </div>
    </div>
    <hr>
    <div class="control">
      <button class="control__button control__button_accept"
              @click="$emit('change', newName, newDescription, index)"></button>
      <button class="control__button control__button_cancel"
              @click="$emit('close')"></button>
    </div>
  </div>
</template>

<script>
import cInput from '@/components/elements/c-input';
import cTextarea from '@/components/elements/c-textarea';

export default {
  name: 'dialogChange',
  components: {
    cInput,
    cTextarea,
  },
  props: ['inItem'],
  data() {
    return {
      inputName: this.inItem.name,
      inputDescription: this.inItem.description,
      index: this.inItem.index,
      newName: '',
      newDescription: '',
    }
  }
}
</script>

<style lang="scss" scoped>
.dialog-change {
  position: fixed;
  padding: 10px;
  padding-top: 20px;
  top: 30%;
  left: calc(50% - 250px);
  width: 500px;
  height: auto; //200px;
  border: 2px solid grey;
  border-radius: 5px;
  background-color: white;
  box-shadow: 1px 1px 1px black;
  box-sizing: border-box;
  
  .body {
    display: flex;
    align-items: center;
    &__images {
      width: 50px;
      margin-right: 10px;
    }
    &-input {
      display: block;
      width: 100%;
      &__input { margin-bottom: 10px; }
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