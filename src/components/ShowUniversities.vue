<template>
    <div class="container">

        <search :msg="SearchByCountryMsg" @search="getDataByCountry" />

        <search :msg="SearchUniversityMsg" @search="filterCountry" />
         <button type="button" @click="SelectedUniversities">refresh selected items</button> 
        <UniversitiesList :universities="showData"  @changeChecked="changeChecked"/>



    </div>
</template>

<script>





// import $ from 'jquery'
import Search from './Search.vue'
import UniversitiesList from './UniversitiesList.vue'
import $ from 'jquery'

export default {
    data() {
        return {
            receivedData:[],
            showData: [],
            SearchUniversityMsg:'Search University from below list: ',
            SearchByCountryMsg: 'Country Name: ',
        }
    },

    components: {
      Search,
      UniversitiesList
    },

    methods: {
        getDataByCountry(country) {
            let requestUrl = 'http://localhost:8000/api/searchbycountry/' +  country
    
            fetch(requestUrl)
                .then(response => ( response.text()))
                .then((response) => {
                    
                    const obj = JSON.parse(response)

                    // add checked status for each item
                    obj.content.forEach( function(item){
                        item.checked=false
                    }
                    )
                    this.receivedData = obj.content
                    this.showData = obj.content
                    console.log(obj.content)


            // console.log(obj.content)
        })
        },

        filterCountry(val){
            if(val != ''){
                let newShowDate =  this.receivedData.filter((data) => data.name.toLowerCase().includes( val.toLowerCase()) || data.domains.toLowerCase().includes(val.toLowerCase()));
                this.showData = newShowDate
            }else{
                this.showData = this.receivedData
            }            
        },



        SelectedUniversities(){


            
                let newShowData = this.showData.filter((data) => data.checked == true);
                

                var dataString = JSON.stringify(newShowData);

                // this will NOT refer to the Vue instance once inside the ajax callback.
                var self = this 
                $.ajax({
                url: 'http://localhost:8000/api/freshuniversities',
                data: {myData: dataString},
                type: 'post',
                success: function(response) {

                    let universities = JSON.parse(response)

                    universities.forEach(niversity => {
                        self.showData.forEach( (item) => {
                        if(item.name == niversity.name){
                            item.webpages = niversity.webpages
                        } 
                        })
                    })


                    
 
                }
                });
       
        },


        changeChecked(val1, val2){

            this.showData.forEach(item=>{
                if(item.name === val1)
                    item.checked = !val2
            })
            
        }
            
        
        


    },

}
</script>

<style scoped>
    .container{
        width: 80%;
        margin: 0 auto;
        padding: 20px;
        height:100%;

    }
</style>