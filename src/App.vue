<template>
  <div class="generalTitleContainer">
    <h2>MUSCODE App</h2>
  </div>
  <div class="dataContainer">
    <ToDoList :toDoList="toDoList" @addToDo="newToDo" />
    <ProductList :productList="productList" />
  </div>
  <div class="container_grid">
    <IteamView
      v-for="product in productList"
      :key="product.key"
      :product="product"
      :optionSelect="optionSelect"
      @editProduct="editProduct"
    />
  </div>
</template>

<script>
import IteamView from "./components/IteamView.vue";
import ToDoList from "./components/ToDoList.vue";
import ProductList from "./components/ProductList.vue";

export default {
  name: "App",
  data() {
    return {
      productList: [
        {
          id: 0,
          name: "iPhone 6s Plus 16GB",
          salePrice: "649",
          price: "1000",
          value: "$",
          key: "0",
          img: "img1.png",
        },
        {
          id: 1,
          name: "iPad Pro 32GB",
          salePrice: "600",
          price: "800",
          value: "$",
          key: "1",
          img: "img2.png",
        },
        {
          id: 2,
          name: "MacBook Pro",
          salePrice: "",
          price: "8000",
          value: "PLN",
          key: "2",
          img: "img3.png",
        },
      ],
      toDoList: [
        { id: 0, name: "Lorem ipsum dolor sit amet, consectetum", done: true },
        { id: 1, name: "Sed do eiusmod tempor ineididunt", done: false },
        { id: 2, name: "Labore et dolore magna aligua", done: false },
        { id: 3, name: "Sed ut perspectis unde omnis iste natus", done: true },
        { id: 4, name: "Minima veniam, quis nostrum exercitationem", done: false},
      ],
      optionSelect: [
        { id: 0, name: "$", key: "$" },
        { id: 1, name: "PLN", key: "PLN" },
        { id: 2, name: "EUR", key: "EUR" },
      ],
    };
  },
  components: {
    ToDoList,
    ProductList,
    IteamView,
  },
  methods: {
    newToDo(el) {
      this.toDoList.push({ id: this.toDoList.length, name: el, done: false });
    },
    editProduct(element) {
      this.productList.find((el) => element.id == el.id).name = element.name;
      this.productList.find((el) => element.id == el.id).price = element.price;
      this.productList.find((el) => element.id == el.id).salePrice = element.salePrice;
      this.productList.find((el) => element.id == el.id).value = element.value;
    },
  },
};
</script>

<style lang="scss">
.generalTitleContainer {
  margin: 30px;
}

.container_grid {
  display: grid;

  place-items: center;
  grid-template-columns: repeat(3, 1fr);
  column-gap: 10px;
  row-gap: 10px;
  align-items: start;
}

.dataContainer {
  width: 100%;
  display: grid;
  grid-template-columns: 1fr 2fr;
  grid-gap: 10px;
  column-gap: 10px;
  align-items: center;
  margin-bottom: 10px;
}

.p {
  color: #384a5c;
  font-size: 14px;
}

.b {
  color: #384a5c;
  font-size: 14px;
  margin: 0;
}

.h1 {
  color: #333;
}

#app {
  font-family: Roboto;
  font-weight: 300;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0;
}

html {
  background-color: #f5f8fa;
  width: 100%;
  max-width: 1180px;
  height: 100%;
}
</style>
