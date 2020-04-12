<template>
    <v-container>
        <v-layout row wrap justify-center pt-4>
            <v-flex md4 px-2>
                <v-form lazy-validation ref="searchform" v-model="valid">
                    <v-text-field
                        append-icon="search"
                        label="Search by product type"
                        solo
                        v-model="productType"
                        @input="searchProduct()"
                    >
                    </v-text-field>
                </v-form>
            </v-flex>
            <v-flex md4 px-2>
                <v-form lazy-validation ref="searchform2" v-model="valid">
                    <v-text-field
                        append-icon="search"
                        label="Search by brand"
                        solo
                        v-model="brand"
                        @input="searchProduct()"
                    >
                    </v-text-field>
                </v-form>
            </v-flex>
        </v-layout>
        <v-layout mt-12 row wrap v-if="loader">
            <v-flex md3 pa-3 v-for="i in 20" :key="i">
                <v-skeleton-loader type="card"> </v-skeleton-loader>
            </v-flex>
        </v-layout>
        <v-layout mt-12 row wrap v-else>
            <v-flex> </v-flex>
            <v-flex md3 pa-3 v-for="i in products" :key="i.id">
                <v-hover v-slot:default="{ hover }">
                    <v-card class="" :href="i.product_link" target="_blank">
                        <div class="pa-6">
                            <v-chip dark small class="orange">
                                {{ i.brand }}
                            </v-chip>
                            <img
                                class="my-8"
                                :src="i.image_link"
                                width="100%"
                                alt=""
                            />
                            {{ i.name }}<br />
                            {{ i.price_sign }}{{ i.price }}<br />
                        </div>
                        <v-expand-transition>
                            <div
                                v-if="hover"
                                class="d-flex transition-fast-in-fast-out orange darken-2 v-card--reveal display-3 white--text"
                                style="height: 100%;"
                            >
                                <v-btn
                                    class="view"
                                    :href="i.product_link"
                                    target="_blank"
                                    >view
                                </v-btn>
                            </div>
                        </v-expand-transition>
                    </v-card>
                </v-hover>
            </v-flex>
        </v-layout>
    </v-container>
</template>
<script>
export default {
    data() {
        return {
            products: [],
            productType: "",
            brand: "",
            loader: true,
        };
    },
    mounted() {
        this.getProducts();
    },
    methods: {
        getProducts() {
            this.axios
                .get("https://makeup-api.herokuapp.com/api/v1/products.json")
                .then((response) => {
                    console.log(response);
                    this.products = response.data;
                    this.loader = false;
                })
                .catch((error) => {
                    console.log(error);
                });
        },
        searchProduct() {
            this.loader = true
            this.axios
                .get(
                    "https://makeup-api.herokuapp.com/api/v1/products.json?product_type=" +
                        this.productType +
                        "&brand=" +
                        this.brand
                )
                .then((response) => {
                    console.log(response);
                    this.products = response.data;
                    this.loader = false;
                })
                .catch((error) => {
                    console.log(error);
                });
        },
    },
};
</script>

<style scoped>
.view-btn {
    background-color: orange !important;
}
.v-card--reveal {
    align-items: center;
    bottom: 0;
    justify-content: center;
    opacity: 0.8;
    position: absolute;
    width: 100%;
}
.view {
    position: relative;
    z-index: 999999 !important;
}
</style>
