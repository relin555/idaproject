<template>
  <form action="" class="form" @submit.prevent="onSubmit">
    <div class="form__input-wrapper">
      <div class="form__input-title-wrapper">
        <p class="form__input-title">Наименование товара</p>
        <div class="form__input-title-dot"></div>
      </div>
      <input
        class="form__input"
        :class="{ 'form__input-active': !isActive.isTitle }"
        type="text"
        :placeholder="placeholder.title"
        v-model="model.title"
        autocomplete="off"
      />
      <label
        class="form__label"
        :class="{ 'form__label-activ': !isActive.isTitle }"
        for="id"
      >
        Поле является обязательным
      </label>
    </div>
    <div class="form__input-wrapper">
      <div class="form__input-title-wrapper">
        <p class="form__input-title">Описание товара</p>
        <div class="form__input-title-dot"></div>
      </div>
      <textarea
        class="form__textarea"
        v-model="model.textarea"
        :placeholder="placeholder.textarea"
      >
      </textarea>
      <label class="form__label" for="id">Поле является обязательным</label>
    </div>
    <div class="form__input-wrapper">
      <div class="form__input-title-wrapper">
        <p class="form__input-title">Ссылка на изображение товара</p>
        <div class="form__input-title-dot"></div>
      </div>
      <input
        class="form__input"
        :class="{ 'form__input-active': !isActive.isLink }"
        type="text"
        :placeholder="placeholder.link"
        v-model="model.link"
        autocomplete="off"
      />
      <label
        class="form__label"
        :class="{ 'form__label-activ': !isActive.isLink }"
        for="id"
        >Поле является обязательным</label
      >
    </div>
    <div class="form__input-wrapper">
      <div class="form__input-title-wrapper">
        <p class="form__input-title">Цена товара</p>
        <div class="form__input-title-dot"></div>
      </div>
      <input
        class="form__input"
        :class="{ 'form__input-active': !isActive.isPrice }"
        type="number"
        :placeholder="placeholder.price"
        v-model="model.price"
        autocomplete="off"
      />
      <label
        class="form__label"
        :class="{ 'form__label-activ': !isActive.isPrice }"
        for="id"
        >Поле является обязательным</label
      >
    </div>

    <button class="form__btn" :disabled="isDisabled">Добавить товар</button>
  </form>
</template>

<script>
export default {
  name: "FormVue",
  data() {
    return {
      placeholder: {
        title: "Введите наименование товара",
        textarea: "Введите описание товара",
        link: "Введите ссылку",
        price: "Введите цену",
      },
      model: {
        id: Date.now(),
        title: null,
        textarea: null,
        link: null,
        price: null,
      },
      isActive: {
        isTitle: true,
        isTextarea: true,
        isLink: true,
        isPrice: true,
      },
      disabled: true,
    };
  },
  methods: {
    onSubmit() {
      this.model.id = Date.now();
      this.$emit("addCard", this.model);
      this.model = {
        title: null,
        textarea: null,
        link: null,
        price: null,
      };
      this.isActive = {
        isTitle: true,
        isTextarea: true,
        isLink: true,
        isPrice: true,
      };
    },
  },
  computed: {
    isDisabled() {
      if (this.model.title === "" || this.model.title === null) {
        return true;
      } else if (this.model.link === "" || this.model.link === null) {
        return true;
      } else if (this.model.price === "" || this.model.price === null) {
        return true;
      }
    },
  },
  watch: {
    model: {
      handler(newTitle, oldTitle) {
        if (newTitle.title === "") {
          this.isActive.isTitle = false;
        } else {
          this.isActive.isTitle = true;
        }
        if (newTitle.textarea === "") {
          this.isActive.isTextarea = false;
        } else {
          this.isActive.isTextarea = true;
        }
        if (newTitle.link === "") {
          this.isActive.isLink = false;
        } else {
          this.isActive.isLink = true;
        }
        if (newTitle.price === "") {
          this.isActive.isPrice = false;
        } else {
          this.isActive.isPrice = true;
        }
      },
      deep: true,
    },
  },
};
</script>

<style lang="scss" scoped>
.form {
  padding: 24px;
  background: #fffefb;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  position: sticky;
  top: 24px;
  width: 332px;
  &__input-wrapper {
    display: flex;
    flex-direction: column;
  }
  &__input-wrapper:nth-child(2) > &__input-title-wrapper > &__input-title-dot {
    display: none;
  }
  &__textarea {
    display: flex;
    height: 108px;
    padding: 10px 16px;
    background: #fffefb;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    border: none;
    resize: none;
    outline: none;
  }
  &__textarea::placeholder {
    font-size: 12px;
    color: #b4b4b4;
  }
  &__input-title-wrapper {
    display: flex;
  }
  &__input-title {
    font-weight: 400;
    font-size: 10px;
    line-height: 13px;
    letter-spacing: -0.02em;
    color: #49485e;
    margin-bottom: 4px;
  }
  &__input-title-dot {
    height: 4px;
    width: 4px;
    background: #ff8484;
    border-radius: 2px;
  }
  &__input {
    padding: 9px 15px 10px 15px;
    background: #fffefb;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    line-height: 15px;
    border: 1px solid rgba(0, 0, 0, 0);
  }
  &__input-active {
    border: 1px solid #ff8484;
  }
  &__input::placeholder {
    font-size: 12px;
    color: #b4b4b4;
  }
  &__label {
    font-size: 8px;
    line-height: 10px;
    letter-spacing: -0.02em;
    color: #ff8484;
    padding: 4px 0 2px 0;
    opacity: 0;
  }
  &__label-activ {
    opacity: 1;
  }
  &__btn {
    background: #7bae73;
    border-radius: 10px;
    width: 100%;
    margin-top: 8px;
    padding: 10px 95px;
    border: none;
    color: #ffffff;
    font-weight: 600;
    font-size: 12px;
    line-height: 15px;
    letter-spacing: -0.02em;
  }
  &__btn:disabled {
    background: #eeeeee;
    color: #b4b4b4;
    cursor: not-allowed;
  }
}
</style>
