<template>
    <div class="productListContainer">
        <div class="titleContainer">
            <p>Lista produktów</p>
        </div>
        <div class="tabele">
            <table>
                <thead>
                    <tr>
                        <th>#</th>
                        <th>NAZWA</th>
                        <th>PROMOCYJNA CENA</th>
                        <th>CENA</th>
                        <th>WALUTA</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="product in productList" :key="product.key">
                        <td>{{ product.id }}</td>
                        <td>{{ product.name }}</td>
                        <td>{{ product.salePrice }}</td>
                        <td>{{ product.price }}</td>
                        <td>{{ product.value }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
export default {
    name: "ProductList",
    props: {
        productList: {
            type: Array,
        },
    },
};
</script>

<style lang="scss" scoped>
.titleContainer {
    text-align-last: left;
    margin: 0 10px;
}
.tabele {
    margin: 0;
    padding: 10px 10px 10px 10px;
}
.tabele table {
    width: 100%;
    border-collapse: collapse;
}
.tabele tr {
    background: #000;
    background: rgba(255, 255, 255, 0.3);
    border-bottom: solid 1px #b2b2b2;
    text-align: left;
}
.tabele tbody tr {
    background: rgba(255, 255, 255, 0.1);
}
.tabele tbody tr:hover {
    background: #f5f8fa;
}
.tabele td {
    padding: 8px 4px;
    text-align: left;
}
.productListContainer {
    box-shadow: 0 0 15px 0px #adadad;
    background-color: #ffffff;
    border: 1px solid #b2b2b2;
    border-radius: 8px;
    height: -webkit-fill-available;
}
</style>
