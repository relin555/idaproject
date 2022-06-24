<template>
  <div class="card">
    <div class="card__delete-btn" @click="deleteCard()">
      <img class="card__delete-icon" src="../assets/icon/delete.svg" alt="">
    </div>
    <img class="card__img" :src="`${item[2]}`" alt="">
    <div class="card__description">
      <h2 class="card__description-title"> {{ item[0] }} </h2>
      <p class="card__description-subtitle">  {{ item[1] }}</p>
      <p class="card__price"> {{ Math.round(item[3]).toLocaleString('ru') }} руб.</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CardProduct',
  props: {
    item: {
      type: Array
    }
  },
  methods: {
    deleteCard() {
      this.$emit('deleteCard')
    }
  },
}
</script>

<style lang="scss" scoped>
  .card {
    position: relative;
    background: #FFFEFB;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
    display: flex;
    flex-direction: column;
    margin: 0 16px 16px 0;
    &__delete-btn {
      position: absolute;
      box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
      border-radius: 10px;
      background: #FF8484;
      display: flex;
      justify-content: center;
      align-items: center;
      right: -8px;
      top: -8px;
      padding: 8px;
      opacity: 0;
      transition: .4s;
      cursor: pointer;
    }
    &__img {
      height: 200px;
      width: 332px;
      border-top-left-radius: 4px;
      border-top-right-radius: 4px;
    }
    &__description {
      padding: 16px 16px 24px 16px;
    }
    &__description-title {
      font-weight: 600;
      font-size: 20px;
      line-height: 25px;
      margin-bottom: 16px;
    }
    &__description-subtitle {
      font-size: 16px;
      line-height: 20px;
      margin-bottom: 32px;
      height: 80px;
      overflow: auto;
      width: 300px;
    }
    &__price {
      font-weight: 600;
      font-size: 24px;
      line-height: 30px;
    }
  }
  .card:nth-child(3n) {
    margin-right: 0px;
  }
  .card:hover > .card__delete-btn {
    opacity: 1;
    transition: .4;
  }
</style>