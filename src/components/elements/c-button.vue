<template>
  <div class="c-button">
    <button class="c-button__button"
            :class="{'c-button__load': isLoad}"
            @click="$emit('click')"><slot></slot></button>
  </div>  
</template>

<script>
export default {
  name: 'cButton',
  props: ['inIsLoad'],
  computed: {
    isLoad() { return (this.inIsLoad == true) ? true : false; }
  }
}
</script>

<style lang="scss" scoped>
.c-button {
  display: flex;
  align-items: center;
  &__button {
    width: 100%;
    padding: 5px;
    border: 1px solid darkblue;
    background-color: rgb(54, 96, 146);

    font-family: 'Montserrat';
    font-size: 12px;
    color: white;
    text-transform: uppercase;
    outline: none;
    cursor: pointer;
    &:hover {
      background-color: rgb(54, 96, 146, .8);
    }
  }
  &__load {
    background-image: url('~@/assets/images/load.gif');
    background-size: 12px 12px;
    background-repeat: no-repeat;
    background-position: 99% center;
  }
}
</style>