<template>
    <div id="app">
        <div class="container">
            <template v-for="(item, index) in items">
                <ListItem :key="index" :item="item" @incrementCart="incrementCart"></ListItem>
            </template>
        </div>
    </div>
</template>

<script>
    import ListItem from "./components/ListItem";

    export default {
        name: 'app',
        components: {
            ListItem
        },
        data() {
            return {
                items: [
                    {
                        id: 0,
                        img: '1.jpg',
                        name: 'Blue Chair',
                        description: 'This is the first item in my list, which is blue chair, its cost is 1500 ',
                        cost: 1500,
                        cart: 0
                    },
                    {
                        id: 1,
                        img: '2.jpg',
                        name: 'White Chair',
                        description: 'This is the second item in my list, which is white chair, its cost is 1300 ',
                        cost: 1300,
                        cart: 0
                    },
                    {
                        id: 2,
                        img: '3.jpg',
                        name: 'Black Chair',
                        description: 'This is the third item in my list, which is black chair, its cost is 2000 ',
                        cost: 2000,
                        cart: 0
                    }, {
                        id: 3,
                        img: '1.jpg',
                        name: 'Blue Chair',
                        description: 'This is the fourth item in my list, which is blue chair, its cost is 1500 ',
                        cost: 1500,
                        cart: 0
                    },
                    {
                        id: 4,
                        img: '2.jpg',
                        name: 'White Chair',
                        description: 'This is the fifth item in my list, which is white chair, its cost is 1300 ',
                        cost: 1300,
                        cart: 0
                    },
                    {
                        id: 5,
                        img: '3.jpg',
                        name: 'Black Chair',
                        description: 'This is the first sixth in my list, which is black chair, its cost is 2000 ',
                        cost: 2000,
                        cart: 0
                    }
                ]
            }
        },
        methods: {
            incrementCart(id) {
                this.items.filter(item => item.id == id)[0].cart ++;
            }
        }
    }
</script>

<style scoped>
    .container {
        width: 80%;
        max-width: 1120px;
        margin: auto;
    }
</style>
