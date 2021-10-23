<template>
    <div v-show="isFull">
        <h3>Корзина</h3>
        <div 
            v-for="element, i in basket" :key=i
        >
            {{element}}
        </div>
        <button 
            @click="$emit('clear-basket')"
            class="button">
            Очистить корзину
        </button>
    <hr>
    </div>
</template>

<script>
export default {
    name: 'Basket',
    props: {
        basket: {
            type: Array,
            default: () => []
        }
    },
    computed: {
        isFull() {
            console.log(this.basket.length)
            return this.basket.length > 0
        }
    }
}
</script>

<style scoped>

.button {
    margin-top: 20px;
    margin-bottom: 20px;
}
</style>