<template>
  <form action="" class="form" @submit.prevent="onSubmit">
    <div class="form__input-wrapper" v-for="(item, id) in inputValue" :key="id">
      <div class="form__input-title-wrapper">
        <p class="form__input-title">
        {{ item.title }}
        </p>
        <div class="form__input-title-dot"></div>
      </div>
      <input class="form__input" :type="item.type" :placeholder="item.placeholder" v-model="item.model" :id="id" autocomplete="off"/>
      <textarea class="form__textarea" name="" id="" :placeholder="item.title" v-model="item.model"></textarea>
      <label class="form__label" :for="id">Поле является обязательным</label>
    </div>
    <button class="form__btn">Добавить товар</button>
  </form>
</template>

<script>
export default {
  name: 'FormVue',
  props: {
    inputValue: {
      type: Array,
      default: []
    },
  },
  methods: {
    onSubmit() {
      this.$emit('addCard')
    }
  },
}
</script>

<style lang="scss" scoped>
  .form {
    padding: 24px;
    background: #FFFEFB;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
    position: fixed;
    top: 83px;
    &__input-wrapper {
    display: flex;
    flex-direction: column;
    }
    &__input-wrapper > textarea {
      display: none;
    }
    &__input-wrapper:nth-child(2) > &__input-title-wrapper > &__input-title-dot {
      display: none;
    }
    &__input-wrapper:nth-child(2) > input {
      height: 108px;
      display: flex;
      flex-direction: column;
      align-items: flex-start;
    }
    &__input-wrapper:nth-child(2) > input::placeholder {
      color: #FF8484;
      display: flex;
      flex-direction: column;
    }
    &__input-wrapper:nth-child(2) > input {
      display: none;
    }
    &__input-wrapper:nth-child(2) > textarea {
      display: flex;
      height: 108px;
      padding: 10px 16px;
      background: #FFFEFB;
      box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
      border-radius: 4px;
      border: none;
      resize: none;
      outline: none;
      margin-bottom: 16px;
    }
    &__input-wrapper:nth-child(2) > textarea::placeholder {
      font-weight: 400;
      font-size: 12px;
      line-height: 15px;
      color: #B4B4B4;
    }
    &__input-wrapper:nth-child(2) > label {
      display: none;
    }
    &__input-title-wrapper {
      display: flex;
    }
    &__input-title {
      font-weight: 400;
      font-size: 10px;
      line-height: 13px;
      letter-spacing: -0.02em;
      color: #49485E;
      margin-bottom: 4px;
    }
    &__input-title-dot {
      height: 4px;
      width: 4px;
      background: #FF8484;
      border-radius: 2px;
    }
    &__input {
      padding: 10px 16px 11px 16px;
      background: #FFFEFB;
      box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
      border-radius: 4px;
      line-height: 15px;
    }
    
    &__input::placeholder {
      font-size: 12px;
      color: #B4B4B4;
    }
    &__label {
      font-size: 8px;
      line-height: 10px;
      letter-spacing: -0.02em;
      color: #FF8484;
      padding: 4px 0 2px 0;
      opacity: 0;
    }
    &__btn {
      background: #EEEEEE;
      border-radius: 10px;
      width: 100%;
      margin-top: 8px;
      padding: 10px 96px;
      border: none;
      color: #B4B4B4;
      font-weight: 600;
      font-size: 12px;
      line-height: 15px;
      letter-spacing: -0.02em;
    }
  }
  
</style>
