<template>
  <div class="dialog">
    <h3 class="dialog__title">Delete position</h3>
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
@import '__dialog.scss';

.dialog {
  z-index: 999;
}
</style>