<template>
  <div class="app">
    <header class="header">
      <div class="header__inner">
        <h1 class="header__title" @click="menuPhone">{{ title }}</h1>
        <div class="header__selected-wrapper">
          <select class="header__selected-options" v-model="selected">
            <option disabled value="">По умолчанию</option>
            <option
              class="header__selected-option"
              v-for="item in options"
              :key="item.value"
              :value="item.value"
            >
              {{ item.select }}
            </option>
          </select>
        </div>
      </div>
    </header>
    <main class="main">
      <aside
        class="main__form-wrapper"
        :class="{ 'main__form-wrapper-active': isMenuPhone }"
      >
        <form-vue
          @addCard="addCard"
          @closeFormPhone="closeFormPhone"
          class="main__form-phone-position"
          :style="{ left: widthleftMenu }"
          :class="{ 'main__form-active': isMenuPhone }"
        />
      </aside>
      <transition-group
        class="main__content-wrapper"
        enter-active-class="cardList-anim-in"
        leave-active-class="cardList-anim-out"
        tag="div"
        mode="out-in"
      >
        <card-product
          v-for="(item, id) in sortCard"
          :key="item.id"
          :item="item"
          @deleteCard="deleteCard(id)"
        />
      </transition-group>
    </main>
  </div>
</template>

<script>
import CardProduct from './components/cardProduct.vue';
import FormVue from "./components/formVue.vue";

export default {
  name: "App",
  components: {
    FormVue,
    CardProduct,
  },
  data() {
    return {
      title: "Добавление товара",
      selected: "",
      isMenuPhone: false,
      widthleftMenu: null,
      options: [
        { select: "По умолчанию", value: "default" },
        { select: "По цене max", value: "max" },
        { select: "По цене min", value: "min" },
        { select: "По наименованию", value: "name" },
      ],
      card: [],
    };
  },
  methods: {
    addCard(model) {
      this.card.push(model);
      this.localCard();
      this.isMenuPhone = false;
    },
    deleteCard(id) {
      this.card.splice(id, 1);
      this.localCard();
    },
    localCard() {
      localStorage.setItem("card", JSON.stringify(this.card));
    },
    menuPhone() {
      this.isMenuPhone = !this.isMenuPhone;
    },
    closeFormPhone() {
      this.isMenuPhone = !this.isMenuPhone;
    },
  },
  computed: {
    sortCard() {
      return this.card.sort((a, b) => {
        if (this.selected === "min") {
          return a.price - b.price;
        }
        if (this.selected === "max") {
          return b.price - a.price;
        }
        if (this.selected === "name") {
          let titleA = a.title.toLowerCase(),
            titleB = b.title.toLowerCase();
          if (titleA < titleB) return -1;
          if (titleA > titleB) return 1;
          return 0;
        }
      });
    },
  },
  watch: {
    isMenuPhone(newOpen , oldClosed) {
      if(newOpen) {
        this.widthleftMenu = ((this.widthBody - this.putFormWidth) / 2) + 'px'
      }
      if(!newOpen) {
        this.widthleftMenu = 101 + '%'
      }
    },
  },
  mounted() {
    const data = localStorage.getItem("card");
    if (data) {
      this.card = JSON.parse(data);
    }
    let getBody = document.querySelector('body')
    let getForm = document.querySelector('.main__form-phone-position')
    this.widthBody = getBody.clientWidth
    this.putFormWidth = getForm.clientWidth
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@600&family=Source+Sans+Pro:wght@400;600&display=swap");
*,
*::after,
*::before {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: "Source Sans Pro", sans-serif;
  color: #3f3f3f;
  font-weight: 400;
  line-height: 15px;
  font-size: 12px;
}
body {
  max-width: 1440px;
  margin: 0 auto;
}
button {
  font-family: "Inter", sans-serif;
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
  &__selected-wrapper {
    position: relative;
  }
  &__selected-wrapper:after {
    content: "";
    background: url("./assets/icon/arrowdown.svg") no-repeat;
    position: absolute;
    pointer-events: none;
    width: 8px;
    height: 5px;
    top: 16px;
    right: 16px;
  }
  &__selected-wrapper > select {
    appearance: none;
    -webkit-appearance: none;
  }
  &__selected-options {
    width: 121px;
    border: none;
    font-size: 12px;
    color: #b4b4b4;
    outline: none;
    background: #fffefb;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    padding: 10px 0px 10px 16px;
    cursor: pointer;
  }
  &__title {
    font-weight: 600;
    font-size: 28px;
    line-height: 35px;
  }
}
.main {
  padding: 0 32px;
  display: flex;
  position: relative;
  &__content-wrapper {
    padding-left: 16px;
    display: flex;
    flex-wrap: wrap;
  }
}

// animation list

.cardList-anim-in {
  animation: activeList 0.5s;
}
.cardList-anim-out {
  animation: activeList 0.5s;
}

@keyframes activeList {
  0% {
    transform: translateX(100px);
  }
  100% {
    transform: translateX(0px);
  }
}

// style ipad

@media (max-width: 1439px) {
  body {
    max-width: 1024px;
    margin: 0 auto;
  }
  .header {
    &__inner {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 20px 20px 10px 20px;
    }
    &__title {
      padding: 5px;
      border-radius: 4px;
      background: #fffefb;
      box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    }
  }
  .main {
    padding: 20px 32px;
    &__content-wrapper {
      padding-left: 10px;
      justify-content: center;
    }
  }
}

//style phone

@media (max-width: 590px) {
  body {
    max-width: 590px;
    margin: 0 auto;
  }
  .header {
    &__inner {
      position: fixed;
      width: 100%;
      z-index: 10;
    }
    &__title {
      font-weight: 600;
      font-size: 16px;
      line-height: 25px;
    }
  }
  .main {
    padding: 10px 15px;
    display: flex;
    position: relative;
    &__content-wrapper {
      padding-left: 10px;
      padding-top: 75px;
      z-index: 5;
    }
    &__form-wrapper {
      opacity: 0;
      position: fixed;
      z-index: 0;
      top: 70px;
      z-index: 1;
      transition: 0.3s;
    }
    &__form-wrapper-active {
      opacity: 1;
      left: 0;
      top: 0;
      z-index: 10;
      width: 100%;
      height: 100%;
      background: rgba(238, 238, 238, 0.6);
      transition: 0.3s;
    }
    &__form-active {
      left: 50px;
    }
  }
}
</style>
