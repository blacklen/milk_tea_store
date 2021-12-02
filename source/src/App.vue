<template>
	<div class="container-fluid app">
		<div class="row">
			<Store
				:stores='stores'
				:activeStore='activeStore'
				@set-active="setActive"
			/>
			<Menu
				:storeInfo= 'storeInfo'
				:toppingsData = 'toppingsData'
			/>
		</div>
	</div>
</template>

<script>
import Store from './components/Store';
import Menu from './components/Menu';
import storesData from '../../data/stores.json';
import storeProductsData from '../../data/storeProducts.json';
import productsData from '../../data/products.json';
export default {
	name:'App',

	components: {
		Store,
		Menu,
	},

	data() {
		return {
			stores: storesData['stores'],
			activeStore: storesData['stores'][0].id,
			storeProducts : storeProductsData['shopProducts'],
			productsData: productsData['products'],
			storeInfo: {},
			toppingsData: [],
		}
	},

	methods: {
		setActive(id) {
			this.getStoreInfo(id)
			this.activeStore = id
		},

		getStoreInfo(id){
			let storeData = this.stores.find(s => s.id === id);
			let products = this.storeProducts.filter(s => s.shop === id);
			let productsId = [];

			products.map(p => productsId.indexOf(p.product) >=0 ? false : productsId.push(p.product));
			this.storeInfo = {
				id : storeData.id,
				name : storeData.name,
				products : productsId.map(p => this.productsData.find(i => i.id === p)),
			}
		}
	},

  created(){
    this.getStoreInfo(this.activeStore);
    for (let p of this.productsData) {
      let sp = p.toppings.toLowerCase().split(',');
      sp.map(s => this.toppingsData.indexOf(s.trim()) >= 0 ? false : this.toppingsData.push(s.trim()));
    }
  }
}
</script>


<style>
@import url('https://fonts.googleapis.com/css2?family=Tajawal:wght@200;300;400;500;700;800;900&display=swap');
* {
  padding: 0px;
  margin: 0px;
  box-sizing: border-box;
  font-size: 18px;
}

.app {
  background: #eee;
  font-family: 'Tajawal', sans-serif;
}

@media only screen and (max-width: 768px) {
  * {
    font-size: 16px;
  }
}

@media only screen and (max-width: 360px) {
  * {
    font-size: 14px;
  }
}

</style>
