<template>
    <div class="col-sm-9 menu">
        <div class="order">
            <h3 class="store-name">{{storeInfo.name}} Menu</h3>
            <div class="add-on">
                <span class="btn btn-secondary filter" @click="showFilter = !showFilter">Filter</span>
                <span class="sort">
                    <label>Sort By</label>
                                        
                    <span class="dropdown">
                        <select class="btn btn-outline-secondary" v-model="selectedValue">
                            <option v-bind:key="item" v-for="item in filters" :value="item">
                                {{item}}
                            </option>
                        </select>
                    </span>
                </span>
            </div>
            <div v-show="showFilter" class="toppings">
                <h4>Toppings:</h4>
                <div class="items">
                    <li class="item" :key='item' v-for="item in toppingsData">
                        <input type="checkbox" :value="item" v-model="checkedFilters"/>  {{item}}
                    </li>
                </div>
            </div>
            <Products  
                :products = 'storeProducts'
            />   
        </div>
    </div>
</template>

<script>
import Products from './Products'
export default {
    name: "Menu",
    data(){
        return {
            storeProducts : {},
            showFilter : false,
            filters: ['Name (A-Z)', 'Name (Z-A)', 'Price(Low-High)', 'Price(High-Low)'],
            selectedValue: null,
            checkedFilters: []
        }
    },
    components: {
        Products
    },
    props: ["storeInfo", 'toppingsData'],
    watch: { 
      	storeInfo: function(newVal, oldVal) { 
            if(oldVal.id !== newVal.id)
                this.storeProducts = newVal.products
        },
        selectedValue: function(val){
            switch(val){
                case 'Name (A-Z)':
                    this.storeProducts.sort((a, b) => (a.name > b.name) ? 1 : -1)
                    break;
                case 'Name (Z-A)':
                    this.storeProducts.sort((a, b) => (a.name < b.name) ? 1 : -1)
                    break;
                case 'Price(Low-High)':
                    this.storeProducts.sort((a, b) => (a.price > b.price) ? 1 : -1)
                    break;
                case 'Price(High-Low)':
                    this.storeProducts.sort((a, b) => (a.price < b.price) ? 1 : -1)
                    break;
           }   
        },
        checkedFilters: function(val){
            if(!val.length)
                this.storeProducts = this.storeInfo.products
            this.storeProducts = this.storeInfo.products.filter(p => {
                let toppings = p.toppings.toLowerCase()
                for(let i of val){
                    if(!toppings.includes(i))
                        return false
                }
                return true
            })
        }
    },

  created(){
      this.storeProducts = this.storeInfo.products
  }
}
</script>

<style scoped>
    .store-name{
        color: #030933e8;
        text-align: center;
        margin: 1em 0;

    }

    .order{
        margin-left: 3em;
        margin-right: 3em;
    }

    .sort{
        float: right;
    }

    .toppings{
        margin-top: 2em;
        background: white;
        padding: 1em;
    }

    .items{
        display: flex;
        column-gap: 2.5em;
        flex-wrap: wrap;
    }

    .item{
        width: 28%;
        list-style-type: none;
    }

    .sort label{
        color: #030933e8;
        font-weight: bold;
    }

    .filter{
        background: #030933e8;
        padding: 10px 3em;
    }

    .dropdown{
        margin-left: 10px;
    }

    .dropdown select{
        color: #030933e8;
        border-color: #030933e8;
    }

    @media only screen and (max-width: 768px) {
        .filter{
            padding: 10px 2em;
        }
        .dropdown select{
            width: 8em;
        }
        .dropdown select option{
            font-size: 0.8em;
        }
	}

    @media only screen and (max-width: 360px) {
        .filter{
            padding: 10px 1em;
        }
        .dropdown select{
            width: 6em;
        }
        .dropdown select option{
            font-size: 0.8em;
        }
	}

</style>

