<template >
    <div class="container mt-5">
        <div class="row">   
            <div class="col-md-3 mb-3"  v-for="(country,index) in countries" :key="index">
                <div class="card">
                    <img :src="country.flags.png" class="card-img-top" alt="Country Flag">
                    <div class="card-body">
                        <h5 class="card-title">{{ country.name.official }}</h5>
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

export default {
    data() {
        return {
            countriesData:[],
            countries:[],
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
    },  
    mounted() {
        axios.get("https://restcountries.com/v3.1/all").then((res)=>{
            this.countriesData = res.data;
            this.countries = [...this.countriesData];
        }).catch((err)=>{
            console.log(err);
        })
    },
}
</script>
<style >
  
</style>