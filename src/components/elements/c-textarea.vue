<template>
  <div class="c-textarea">
  <label class="c-textarea__title"><slot></slot></label>
  <textarea class="c-textarea__input" 
            rows="5"
            :class="{'c-textarea__input_validation': isEmpty}"
            v-model="inputValue"
            @input="setInputValue"
            @keydown="enterInputValue" />
  </div>
</template>

<script>
export default {
  name: 'cTextarea',
  props: [
  'inValidation',
  'inValue',
  ],
  computed: {
    isEmpty() {return this.inValidation;}
  },
  data: function() {
    return {
      inputValue: '',
    }
  },
  created() {
    this.inputValue = this.inValue;
  },
  methods: {
    setInputValue: function() {
      this.$emit('input', this.inputValue);
    },
    enterInputValue: function(event) {
      this.$emit('keydown', event.key);
    }
  }
}
</script>

<style lang="scss" scoped>
.c-textarea {
  position: relative;
  &__title {
    position: absolute;
    display: flex;
    align-items: flex-end;
    width: 94.5%;
    height: 13px;
    left: 5px;
    top: 1px;
    font-size: 8px;
    text-transform: uppercase;
    background-color: white;
  }
  &__input {
    left: 0px;
    top: 0px;
    width: 100%;
    padding: 3px;
    padding-left: 5px;
    padding-top: 16px;
    font-size: 14px;
    border: 1px solid grey;
    border-radius: 3px;
    box-sizing: border-box;
    resize: none;
    outline: none;
    &:focus {
      box-shadow: 1px 1px 1px lightblue, -1px -1px 1px lightblue;
    }
    &_validation {
      box-shadow: 1px 1px 1px red, -1px -1px 1px red;
    }
  }
}
</style>