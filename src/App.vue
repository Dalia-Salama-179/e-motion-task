<template>
    <div id="app">
        <div class="container">
            <div class="cart-wrapper">
                <a class="cart-icon" @click="showCart = !showCart">
                    <span>
                        {{totalCart}}
                    </span>
                    <svg height="25px" viewBox="0 -31 512.00026 512" width="25px">
                        <path d="m164.960938 300.003906h.023437c.019531 0 .039063-.003906.058594-.003906h271.957031c6.695312 0 12.582031-4.441406 14.421875-10.878906l60-210c1.292969-4.527344.386719-9.394532-2.445313-13.152344-2.835937-3.757812-7.269531-5.96875-11.976562-5.96875h-366.632812l-10.722657-48.253906c-1.527343-6.863282-7.613281-11.746094-14.644531-11.746094h-90c-8.285156 0-15 6.714844-15 15s6.714844 15 15 15h77.96875c1.898438 8.550781 51.3125 230.917969 54.15625 243.710938-15.941406 6.929687-27.125 22.824218-27.125 41.289062 0 24.8125 20.1875 45 45 45h272c8.285156 0 15-6.714844 15-15s-6.714844-15-15-15h-272c-8.269531 0-15-6.730469-15-15 0-8.257812 6.707031-14.976562 14.960938-14.996094zm312.152343-210.003906-51.429687 180h-248.652344l-40-180zm0 0"/>
                        <path d="m150 405c0 24.8125 20.1875 45 45 45s45-20.1875 45-45-20.1875-45-45-45-45 20.1875-45 45zm45-15c8.269531 0 15 6.730469 15 15s-6.730469 15-15 15-15-6.730469-15-15 6.730469-15 15-15zm0 0"/>
                        <path d="m362 405c0 24.8125 20.1875 45 45 45s45-20.1875 45-45-20.1875-45-45-45-45 20.1875-45 45zm45-15c8.269531 0 15 6.730469 15 15s-6.730469 15-15 15-15-6.730469-15-15 6.730469-15 15-15zm0 0"/>
                    </svg>
                </a>
                <ul class="cart-list" v-if="showCart && cartList.length > 0">
                    <li v-for="(item, index) in cartList" :key="index">
                        <a @click.prevent="removeItem(item.id)" class="remove-item">&times;</a>
                        <div>
                            <img :src="require(`@/assets/images/${item.img}`)" alt="">
                            <div>
                                <p>{{item.name}}</p>
                                <p>{{item.cost}}</p>
                                <div class="item-cart-interaction">
                                    <a @click.prevent="incrementCartItem(item.id)">+</a>
                                    <span>{{item.itemsInCard}}</span>
                                    <a @click.prevent="decrementCartItem(item.id)">-</a>
                                </div>
                            </div>
                        </div>
                    </li>
                </ul>
            </div>
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
                ],
                cartList: [],
                showCart: false
            }
        },
        computed: {
            totalCart() {
                let total = 0
                this.cartList.map(item => {
                    total += item.itemsInCard
                })
                return total;
            }
        },
        methods: {
            incrementCart(id) {
                let item = this.items.filter(item => item.id == id)[0];
                item.cart ++;
                if (this.cartList.find(el => el.id == id)) {
                    this.cartList.filter(el => el.id == id)[0].itemsInCard ++;
                } else {
                    this.cartList.push({
                        ...item,
                        itemsInCard: 1
                    })
                }
            },
            incrementCartItem(id) {
                this.items.filter(item => item.id == id)[0].cart ++;
                this.cartList.filter(el => el.id == id)[0].itemsInCard ++;
            },
            decrementCartItem(id) {
                let itemsCart = this.items.filter(item => item.id == id)[0].cart;
                let cartList = this.cartList.filter(el => el.id == id)[0].itemsInCard;
                if (itemsCart > 0) {
                    this.items.filter(item => item.id == id)[0].cart --;
                }
                if (cartList > 0) {
                    this.cartList.filter(el => el.id == id)[0].itemsInCard --;
                }
            },
            removeItem(id) {
                let cartItem = this.cartList.find(item => item.id == id)
                this.cartList.splice(this.cartList.indexOf(cartItem), 1)
                this.items.find(item => item.id == id).cart = 0;
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
    .cart-icon {
        display: inline-flex;
        align-items: center;
        position: relative;
        cursor: pointer;
    }
    .cart-icon span {
        color: red;
        position: absolute;
        top: -12px;
        left: calc(50% - 4px);
        font-weight: bold;
    }
    .cart-icon svg {
        fill: #007bff;
        margin-right: 5px;
    }
    .cart-wrapper {
        margin: 20px 0;
        position: relative;
        text-align: right;
    }
    .cart-list {
        position: absolute;
        right: 0;
        list-style: none;
        width: 230px;
        border-radius: 5px;
        margin: 0;
        padding: 0;
        border: 1px solid #ddd;
        background: #ffffff;

    }
    .cart-list li {
        padding: 10px;
        position: relative;
    }
    .cart-list li > div {
        display: flex;
    }
    .cart-list li img {
        width: 50px;
    }
    .cart-list li:not(:last-of-type) {
        border-bottom: 1px solid #ddd;
    }
    .cart-list p {
        margin: 0;
    }
    .remove-item {
        font-size: 21px;
        position: absolute;
        right: 10px;
        top: 0;
        cursor: pointer;
        color: red;
        font-weight: bold;
    }
    .item-cart-interaction a {
        font-size: 18px;
        display: inline-block;
        border: 1px solid #ddd;
        border-radius: 100%;
        width: 25px;
        line-height: 25px;
        text-align: center;
        cursor: pointer;
    }
    .item-cart-interaction span {
        padding: 0 15px;
    }
</style>
