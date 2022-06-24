<template>
  <header class="header">
    <div class="header__inner">
      <h1 class="header__title"> {{ title }} </h1>
      <div class="header__selected-wrapper">
        <select class='header__selected-options' v-model="selected">
          <option disabled value="">По умолчанию</option>
          <option class="header__selected-option" v-for="item in options" :key="item.value" :value="item.value"> {{ item.select }} </option>
        </select>
      </div>
    </div>
    <main class="main">
      <aside class="main__form-wrapper">
        <form-vue :inputValue="inputValue"/>
      </aside>
      <aside class="main__content-wrapper"></aside>
    </main>
  </header>
</template>

<script>
import FormVue from './components/formVue.vue'

export default {
  name: 'App',
  components: {
    FormVue
  },
  data() {
    return {
      title: 'Добавление товара',
      selected: '',
      options: [
        { select: 'По умолчанию', value: 'default' },
        { select: 'По цене max', value: 'max' },
        { select: 'По цене min', value: 'min' },
        { select: 'По наименованию', value: 'name' },
      ],
      inputValue: [
        { type: 'text', placeholder: 'Введите наименование товара', title: 'Наименование товара'},
        { type: 'text', placeholder: 'Введите описание товара', title: 'Описание товара'},
        { type: 'email', placeholder: 'Введите ссылку', title: 'Ссылка на изображение товара'},
        { type: 'number', placeholder: 'Введите цену', title: 'Цена товара'},
      ]
    }
  }
}
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@600&family=Source+Sans+Pro:wght@400;600&display=swap');
  *, *::after, *::before {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    font-family: 'Source Sans Pro', sans-serif;
    color: #3F3F3F;
    font-weight: 400;
  }
  body {
    max-width: 1440px;
    margin: 0 auto;
  }
  button {
    font-family: 'Inter', sans-serif;
    cursor: pointer;
  }
  input {
    outline: none;
    border: none;
  }
  .header {
    &__inner {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 32px 32px 16px 32px;
    }
    &__title {

    }
    &__selected-options {
      border: none;
      font-size: 12px;
      color: #B4B4B4;
      outline: none;
      background: #FFFEFB;
      box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
      border-radius: 4px;
      padding: 10px 0px 10px 16px;
      cursor: pointer;
    }
  }
  .main {
    padding: 0 32px;
    display: flex;
    position: relative;
  }
</style>
