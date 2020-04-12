<template>
    <v-app>
        <!-- <v-app-bar>
            <v-app-bar-items>
                <v-btn to="/">Home</v-btn>
                <v-btn to="/about">About</v-btn>
            </v-app-bar-items>
        </v-app-bar> -->
        <v-content>
            <div class="header">
                <v-container fill-height>
                    <v-layout row wrap justify-center align-center>
                        <v-flex md7 text-center>
                            <h1 class="text-white head-text font-weight-bold">Online Products Catalogue</h1>

                        </v-flex>
                    </v-layout>
                <router-view></router-view>
                </v-container>
            </div>
        </v-content>
    </v-app>
</template>
<script>
export default {
    data () {
        return {
            valid: true
        }
    }
};
</script>
<style scoped>
.header {
    height: 400px;
    width: 100%;
    background-color: orange;
}
.head-text{
    font-size: 40pt;
}
</style>
