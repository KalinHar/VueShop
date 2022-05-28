<template>
    <div class="column is-3">
        <div class="box">
            <figure class="image mb-4">
                <img v-bind:src="product.get_thumbnail">
            </figure>

            <h3 class="is-size-4">{{ product.name }}</h3>
            <p class="is-size-6 has-text-grey">${{ product.price }}</p>

            <div class="buttons">
                <router-link v-bind:to="product.get_absolute_url" class="button is-info is-light mt-4">View details</router-link>
                <button class="button is-primary is-light mt-4" @click="addToCart()">Add to Cart</button>
            </div>
        </div>
    </div>
</template>

<script>
import { toast } from 'bulma-toast'

export default {
    name: 'ProductBox',
    props: {
        product: Object
    },
    methods: {
        addToCart() {
            if (isNaN(this.quantity) || this.quantity < 1) {
                this.quantity = 1
            }
            const item = {
                product: this.product,
                quantity: this.quantity
            }
            this.$store.commit('addToCart', item)
            toast({
                message: 'The product was added to the cart',
                type: 'is-success',
                dismissible: true,
                pauseOnHover: true,
                duration: 2000,
                position: 'bottom-right',
            })
        }
    }
}
</script>

<style scoped>
  .image {
    margin-top: -1.25rem;
    margin-left: -1.25rem;
    margin-right: -1.25rem;
  }
</style>