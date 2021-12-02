<template>
	<div class="products">
		<div class="card" :key="product.id" v-for="product in products">
		<Product :product="product" />
		</div>
	</div>
</template>

<script>
import Product from './Product.vue';

export default {
	name: "Products",
	components: {
		Product,
	},
	props: ["products"],
}
</script>

<style scoped>
.products {
  margin-top: 3em;
  display: flex;
  column-gap: 2.5em;
  flex-wrap: wrap;
}

.card {
  width: 29%;
  color: #030933e8;
  margin-bottom: 2em;
}

@media only screen and (max-width: 768px) {
  .card {
    width: 45%;
  }
}
@media only screen and (max-width: 360px) {
  .card {
    width: 100%;
  }
}
</style>

