<template>
  <div class="dialog">
    <h3 class="dialog__title">Change position</h3>
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
@import '__dialog.scss';

.dialog {
  z-index: 998;
  .body {
    &-input {
      display: block;
      width: 100%;
      &__input { margin-bottom: 10px; }
    }
  }
}
</style>