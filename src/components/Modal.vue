<template >


      <div  class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog" >
          <div class="modal-content" v-if="country != null">
            <div class="modal-header" >
              <h5 class="modal-title" id="exampleModalLabel">Country Information </h5>
              <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
              <div class="card">
                    <img :src="country.flags.png" class="card-img-top" alt="Country Flag">
                    <div class="card-body">
                        <h5 class="card-title">{{ country.name.official }}</h5>
                        <p class="card-text">2-character Country Code: <span id="cca2">{{ country.cca2 }}</span></p>
                        <p class="card-text">3-character Country Code: <span id="cca3">{{ country.cca3 }}</span></p>
                        <div class="card-text"> 
                            Native Country Name
                            <ul v-for="(nativeName, lang) in country.name.nativeName" :key="lang">
                                <h6>in language : {{lang}}</h6>
                                <li v-for="item in nativeName">{{ item }}</li>
                            </ul>
                        </div>
                        <div class="card-text">
                            Alternative Country Name
                            <ul>
                                <li v-for="item in country.altSpellings">{{ item }}</li>
                            </ul>
                        </div>
                        <p class="card-text">Country Calling Codes: <span id="calling-codes">{{ fullIdd(country.idd) }}</span></p>
                        <div class="card-text">Currencies of the Country : </div>
                        <ul>
                          <li v-for="currency in country.currencies">{{ fullCurrency(currency) }}</li>
                        </ul>
                        <div>capital of the Country  </div>
                        <ul>
                          <li v-for="capital in country.capital">{{ capital }}</li>
                        </ul>
                        <p class="card-text">Region : {{ country.region }}</p>
                        <p class="card-text">Subregion : {{ country.subregion || "N/A" }}</p>
                        <p class="card-text">Continents : {{ allContinents(country.continents) }}</p>
                        <div class="card-text">languages in the Country  </div>
                        <ul>
                          <li v-for="(language,lang) in country.languages">{{ fullLanguage(language,lang) }}</li>
                        </ul>

                        <p>Google Maps : <a :href="country.maps.googleMaps" target="blank">{{ country.maps.googleMaps }}</a></p>

                        <div class="card-text">Timezone of the Country </div>
                        <ul>
                          <li v-for="(timezone,index) in country.timezones" :key="index">{{ timezone }}</li>
                        </ul>

                        <p class="card-text">Start of Week : {{ country.startOfWeek }}</p>
                    </div>
                </div>
            </div>
         
          </div>
        </div>
      </div>
</template>
<script>
export default {
    props:["country"],
    methods:{
      fullIdd(idd){
        return idd.root + idd.suffixes;
      },
      fullCurrency(currency){
        return currency ? `${currency.name} (${currency.symbol})` : "N/A";
      },
      fullLanguage(language,lang){
        return `${lang} : ${language}`;
      },
      allContinents(continents){
        return continents.join(", ");
      }


    }
}
</script>
<style lang="">
    
</style>