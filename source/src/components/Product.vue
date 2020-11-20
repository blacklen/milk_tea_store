<template>
    <div class="card-body">
        <h6 class="card-subtitle mb-2 text-muted">{{product.id}}</h6>
        <h5 class="card-title">{{product.name}}</h5>
        <hr class="gap">
        <h5 class="card-title">Toppings: </h5>
        <p class="card-text">{{product.toppings}}</p>
        <span class="trending">Trending</span>
        <span class="price"> ${{product.price}}</span>
    </div>
</template>

<script>
export default {
    name: "Product",
    props: ["product"],
    methods: {
    
    },
}
</script>

<style scoped>
    .gap{
        border: 2px solid #030933e8;
    }

    .trending{
        background: #030933e8;
        color: white;
        text-align: center;
        padding: 8px;
        margin-top: 10px;
        margin-left: -1.3em;
        font-weight: 300;
    }
    .price{
        float: right;
        font-size: 1.5em;
        font-weight: bold;
    }

</style>

