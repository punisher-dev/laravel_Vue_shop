<template>
    <div>
        <hr>
         <button class="btn btn-warning text-center" 
                v-on:click.prevent="addProductToCart()">
                Add To Cart
        </button>
    </div>
</template>

<script>
import axios from 'axios';

    export default {
        data(){

        },
        props:['productId', 'userId'],
        methods:{
            async addProductToCart(){

                // Checking if user is logged in.
                
                if(this.userId == 0){
                    this.$toastr.e('You Need to login, To add this product in the Cart');
                    return;
                }

                // if user is logged in add item to cart.

                let response = await axios.post('/cart', {
                    'product_id': this.productId
                });

                this.$root.$emit('changeInCart', response.data.items);

            }
        },
        mounted() {
            console.log('Component mounted.')
        }
    }
</script>
