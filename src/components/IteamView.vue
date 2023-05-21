<template>
    <div class="iteamViewContainer" @click="isModalVisible = true">
        <div class="rotate">
            <div v-show="product.salePrice != ''" class="salePrice">
                {{ Math.ceil((product.salePrice * 100) / product.price) - 100 }}%
            </div>
        </div>
        <b class="titleProduct">{{ product.name }}</b>
        <div class="pictureContainer">
            <img :alt="product.img" :style="'width: 20vh; object-fit: cover;'" :src="product.img" />
        </div>
        <div :style="'display: flex; justify-content: center; flex-direction: column; '">
            <b class="salePriceColor">{{ product.salePrice ? product.salePrice : product.price }}
                {{ product.value }}</b>
            <s :style="'margin: 0 0 20px 0; font-size: 14px;'">{{ product.salePrice ? product.price : "" }}
                {{ product.salePrice ? product.value : "" }}</s>
        </div>
    </div>

    <teleport to="#modal">
        <ModalNewProduct @editProduct="editProduct" v-show="isModalVisible" v-model:isModalVisible="isModalVisible"
            :product="product" :optionSelect="optionSelect"></ModalNewProduct>
    </teleport>
</template>

<script>
import ModalNewProduct from "./ModalNewProduct.vue";
export default {
    name: "IteamView",
    components: {
        ModalNewProduct,
    },
    data() {
        return {
            isModalVisible: false,
        };
    },
    props: {
        product: {
            type: Object,
        },
        optionSelect: {
            type: Array,
        },
    },
    methods: {
        editProduct(el) {
            this.$emit("editProduct", {
                id: el.id,
                name: el.name,
                price: el.price,
                salePrice: el.salePrice,
                value: el.value,
            });
        },
    },
};
</script>

<style lang="scss" scoped>
.salePriceColor {
    color: rgb(129, 69, 129) !important;
    margin: 3px;
}
.salePrice {
    width: 117px;
    height: 0px;
    border-left: 22px solid transparent;
    border-right: 22px solid transparent;
    border-bottom: 22px solid #000000;
    color: white;
}
.rotate {
    transform: translateX(180px) rotate(45deg);
    position: sticky;
    overflow: 20;
    width: 52px;
    left: 90px;
}
.titleProduct {
    float: left;
    margin: 20px;
}
.pictureContainer {
    // width: 100%;
    width: 100%;
    height: 300px;
    display: flex;
    align-items: center;
    align-content: center;
    justify-content: center;
}
.fit-picture {
    width: 250px;
}
.iteamViewContainer {
    box-shadow: 0 0 15px 0px #adadad;
    cursor: pointer;
    width: 100%;
    background-color: #ffffff;
    border: 1px solid #b2b2b2;
    border-radius: 8px;
    height: -webkit-fill-available;
    overflow: hidden;
    overflow-y: auto;
    overflow-x: hidden;
    word-wrap: initial;
}
</style>
