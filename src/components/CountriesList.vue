<template >
    <nav class="navbar navbar-light bg-light">
        <div class="container-fluid">
            
            <Sort v-model:temp-countries="tempCountries" :countries-data="countriesData" :display-country="()=>{displayCountry()}"></Sort>            
            <Search :countries-data="countriesData" v-model:countries="countries" :display-country="()=>{displayCountry()}"></Search>
            
        </div>
    </nav>
    <div class="container mt-5">
        <div class="d-flex justify-content-center">
            <Pagination :pages-show="pageShow" v-model:current-page="currentPage" :items-per-page="itemsPerPage" :display-country="()=>{displayCountry()}"/>
        </div>
        <div class="row">   
            <div class="col-md-3 mb-3"  v-for="(country,index) in countries" :key="index">
                <div class="card">
                    <img :src="country.flags.png" class="card-img-top" alt="Country Flag">
                    <div class="card-body">
                        <h5 class="card-title" data-bs-toggle="modal" data-bs-target="#exampleModal" @click="getCountry(country)">{{ country.name.official }}</h5>
                        <p class="card-text">2-character Country Code: <span id="cca2">{{ country.cca2 }}</span></p>
                        <p class="card-text">3-character Country Code: <span id="cca3">{{ country.cca3 }}</span></p>
                        <div class="card-text mt-2">
                            Native Country Name : {{ getNativeName(country) }}
                        </div>
                        <div class="card-text mt-2">
                            Alternative Country Name : {{ country.altSpellings.join(", ") }}
                        </div>
                        <p class="card-text mt-2">Country Calling Codes: <span id="calling-codes">{{ fullIdd(country.idd) }}</span></p>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <Modal :country="selectedCountry"></Modal>
</template>
<script>
import axios from 'axios';
import Modal from './Modal.vue';
import Pagination from './Pagination.vue';
import Sort from './Sort.vue';
import Search from './Search.vue';

export default {
    components:{
        Modal,
        Pagination,
        Sort,
        Search
    },
    data() {
        return {
            countriesData:[],
            countries:[],
            tempCountries:[],

            currentPage:1,
            itemsPerPage:25,
            pageShow:1,

            selectedCountry:null
        }
    }, 
    
    methods:{        
        fullIdd(idd){   
            if(idd.suffixes){
                return idd.root + idd.suffixes;
            }
            else{
                return "N/A"
            }
        },
        getNativeName(country) {
            return country.name.nativeName ? Object.values(country.name.nativeName)[0].common : 'N/A';
        },
        getCountry(country){
            this.selectedCountry = country;
        },
        displayCountry(){            
            const startIndex = (this.currentPage * this.itemsPerPage) - this.itemsPerPage;
            const endIndex = startIndex + this.itemsPerPage;
            this.countries = this.tempCountries.slice(startIndex,endIndex);
        },
    },  
    mounted() {
        axios.get("https://restcountries.com/v3.1/all").then((res)=>{
            this.countriesData = res.data;
            this.tempCountries = [...this.countriesData];
            this.pageShow = Math.ceil(this.countriesData.length / this.itemsPerPage);
            this.displayCountry();
        }).catch((err)=>{
            console.log(err);
        })
    },
}
</script>
<style >
  
</style>