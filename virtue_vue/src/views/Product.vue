<template>
    <div class="page-product">
        <div class="columns is-multiline">
            <div class="column is-9">
                <figure>
                    <img  v-bind:src="product.get_image" height="500" width="600">
                </figure>

               
               
            </div>

            <div class="description"  >
                <h1 class="title">{{ product.name }}</h1>
                <h2 class="subtitle">Descrição</h2>
                

                <p class="text"  >{{ product.description }}</p>
                <br>
                <p><strong>Preço: </strong>R$ {{ formatPrice(product.price) }}</p>

                <div class="field has-addons mt-6">
                    <div class="control">
                        <input type="number" class="input" min="1" v-model="quantity">
                    </div>

                    <div class="control">
                        <a class="button is-dark" @click="addToCart()">Adicionar ao carrinho</a>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import { toast } from 'bulma-toast'

export default {
    name: 'Product',
    data() {
        return {
            product: {},
            quantity: 1
        }
    },
    mounted() {
        this.getProduct() 
    },
    methods: {
        async getProduct() {
            this.$store.commit('setIsLoading', true)

            const category_slug = this.$route.params.category_slug
            const product_slug = this.$route.params.product_slug

            await axios
                .get(`/api/v1/products/${category_slug}/${product_slug}`)
                .then(response => {
                    this.product = response.data

                    document.title = this.product.name + ' | Virtue Shop'
                })
                .catch(error => {
                    console.log(error)
                })

            
            this.$store.commit('setIsLoading', false)
        },

        formatPrice(value) {
        let val = (value/1).toFixed(2).replace('.', ',')
        return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".")
        },
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
                message: 'Produto adicionado ao carrinho!',
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
    .description {
    display: inline-block;
    position: absolute ;
    right: 0;
    width: 30em;
}
    .text{
        padding-right: 3em;
        text-align: justify;
    }
    .image{
        position: left;
        left: 0;
    }
    @media screen and (max-width: 600px) {
        .image{
            position: center;
            margin-bottom: 10em;   
        }
        .description{
            position: center;
            padding-bottom: 5em;
        }
    }

</style>