<template>
  <header class="header">
    <div class="header__inner">
      <h1 class="header__title"> {{ title }} </h1>
      <div class="header__selected-wrapper">
        <select class='header__selected-options' v-model="selected">
          <option disabled value="default">По умолчанию</option>
          <option class="header__selected-option" v-for="item in options" :key="item.value" :value="item.value"> {{ item.select }} </option>
        </select>
      </div>
    </div>
  </header>
</template>

<script>

export default {
  name: 'App',
  components: {
    
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
    }
  }
}
</script>

<style lang="scss">
  *, *::after, *::before {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  .header {
    &__inner {

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
    }
  }
</style>
