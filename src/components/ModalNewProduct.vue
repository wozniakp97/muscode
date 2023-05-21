<template>
    <div class="modal">
        <div class="modal__content">
            <div>
                <div class="titleContainer">
                    <h3>Edycja produktu: {{ product.name }}</h3>
                </div>
                <div class="pictureContainer">
                    <img :alt="product.img" class="imageStyle" :src="product.img" />
                </div>

                <label>Nazwa produktu</label>
                <input type="text" class="inputClass" v-model="name" />

                <label>Cena</label>
                <input type="number" class="inputClass" v-model="price" />

                <label>Promocyjna cena</label>
                <input type="number" class="inputClass" v-model="salePrice" />
                <div :style="'display: flex; flex-direction: column;'">
                    <label>Waluta</label>
                    <select class="inputClassSelected" id="select" v-model="value">
                        <option v-for="option in optionSelect" :key="option.id" :value="option.key">
                            {{ option.name }}
                        </option>
                    </select>
                </div>
            </div>
            <div class="modal__buttons">
                <button :style="'background-color: rgb(129, 69, 129); color:white;'" @click="editProduct">
                    Zapisz
                </button>
                <button :style="'margin-left: 10px;'" @click="cancelEdit(product)">
                    Anuluj
                </button>
            </div>
        </div>
    </div>
</template>

<script>
import { ref } from "vue";
export default {
    name: "MyModal",
    props: {
        isModalVisible: {
            type: Boolean,
            default: true,
        },
        product: {
            type: Object,
        },
        optionSelect: {
            type: Array,
        },  
    },
    setup(props) {
        const id = ref(props.product.id);
        const name = ref(props.product.name);
        const price = ref(props.product.price);
        const salePrice = ref(props.product.salePrice);
        const value = ref(props.product.value);

        return { name, salePrice, price, value, id };
    },
    methods: {
        editProduct() {
            this.$emit("editProduct", {
                id: this.id,
                name: this.name,
                price: this.price,
                salePrice: this.salePrice,
                value: this.value,
            });
            this.$emit("update:isModalVisible", false);
        },
        cancelEdit(product){
            this.name = ref(product.name)
            this.price = ref(product.price)
            this.salePrice = ref(product.salePrice)
            this.value = ref(product.value)
            this.$emit('update:isModalVisible', false)
        }
    },
};
</script>

<style lang="scss" scoped>
.inputClass {
    margin: 6px 5px;
    border: none;
    border-bottom: 1px solid #b2b2b2;
    width: 100%;
    margin: 6px 0;

    &:focus {
        outline: none;
    }

    &:placeholder-shown+.label {
        opacity: 0;
        visibility: hidden;
        transform: translateY(-40px);
    }

    &Selected {
        border: solid white !important;
        border-bottom: #b2b2b2 !important;
    }

    &Selected:focus {
        outline: none;
    }

    &Selected:placeholder-shown+.label {
        opacity: 0;
        visibility: hidden;
        transform: translateY(-40px);
    }
}

label {
    color: #b2b2b2;
    width: 100%;
    margin: 6px 0;
}

.pictureContainer {
    width: 100%;
    height: 300px;
    display: flex;
    align-items: center;
    align-content: center;
    justify-content: center;
}
.imageStyle {
    width: 20vh;
    height: 20vh;
    object-fit: cover;
    box-shadow: 0 0 15px 0px #adadad;
    border-radius: 50%;
}

.titleContainer {
    display: flex;
    border-bottom: solid 3px #6868e6;
}

.modal {
    position: fixed;
    top: 0;
    left: 0px;
    width: 100vw;
    height: 100vh;
    display: flex;
    justify-content: right;
    align-items: center;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 2;

    &__content {
        width: 30%;
        height: 100%;
        background-color: #fff;
        display: flex;
        flex-direction: column;
        padding: 10px;
        justify-content: space-between;
    }

    &__buttons {
        border-top: solid 1px #8e8e8e;
        display: flex;
        justify-content: flex-start;
        padding: 10px 0;
    }
}
</style>
