<template>
   <div class="col-sm-3 store">
        <h3 class="header" > Milk Tea Store </h3>
        <ul :key="store.id" v-for="store in stores" class="nav flex-column text-center">
            <li @click="$emit('set-active', store.id)" :class="{ 'active': activeStore === store.id }" class="nav-item">
                <a class="nav-link" href="#">{{store.name}}</a>
            </li>
        </ul>

    </div>
    
</template>

<script>

export default {
    name: "Store",
    components: {
    },
    props: ["stores", "activeStore"]
}
</script>

<style scoped>
     .store{
        background: #030933e8;
        margin: 0px !important;
        padding: 0px !important;
        min-height: 100vh;
    }
    .header{
        text-align: center;
        color: white;
        padding: 10px 0 20px 0;
    }

    .store a{
        color: grey
    }

    .store a:hover{
      background: #2f366b;
      color: white;
    }

    .active{
        background: #2f366b;
    }

    .active a{
        color: white
    }

</style>

