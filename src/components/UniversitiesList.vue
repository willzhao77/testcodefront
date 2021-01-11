<template>
    <div id="listContainer">

        <table class="" id="listTable">
            <thead>
                <tr>
                    <th>status</th>
                    <th>Name</th>
                    <th>Country</th>
                    <th>Webpages</th>
                    <th>domains</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="item in universities" :key="item.name">
                    <td><input type="checkbox"  :checked="item.checked" v-on:change ="changeChecked(item.name, item.checked)" /></td>
                    <td>{{item.name}}</td>
                    <td>{{item.country}}</td>
                    <td>{{item.webpages}}</td>
                    <td>{{item.domains}}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
<script>



export default {
    data() {
        return {
            showData: []
        }
    },

    props:['universities'],
    methods: {
            changeChecked(val1, val2){
                this.$emit('changeChecked', val1, val2)
            }
        },

  
    


}
</script>

<style scoped>

#listTable {
  font-family: Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

#listTable td, #customers th {
  border: 1px solid #ddd;
  padding: 8px;
}

#listTable tr:nth-child(even){background-color: #f2f2f2;}

#listTable tr:hover {background-color: #ddd;}

#listTable th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: center;
  background-color: #4CAF50;
  color: white;
}



</style>