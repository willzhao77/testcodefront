<template>
    <div class="searchContainer">
        <label>{{msg}}</label>
        <input type="text" v-model="searchText"/>
         <button type="button" @click="searchFunc">Search</button> 
    </div>
</template>

<script>
export default {
    name: 'Search',
    data(){
        return{
          searchText:''  
        }
    },
    props:['msg'],
    methods: {
        searchFunc(){
            this.$emit('search', this.searchText)
        }
    },
}

</script>

<style scoped>
    .searchContainer{

        width: 80%;
        margin: 20px auto;
    }
</style>