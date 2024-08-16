<template >
    <select class="form-select w-25" @change="sortCountry"  aria-label="Default select example" >
        <option value="" selected>sort Country at here</option>
        <option value="asc">Name Country A to Z</option>
        <option value="desc">Name Country Z to A</option>
    </select>
</template>
<script>
export default {
    props:['tempCountries','countriesData','displayCountry'],
    data(){
        return{
            countries:[],
        }
    },
    methods:{
        sortCountry(event){
            
            this.countries = [...this.tempCountries];
            if(event.target.value == "asc"){
                this.countries.sort((a,b)=>a.name.official.localeCompare(b.name.official));
                this.$emit('update:tempCountries',this.countries);
            } 
            else if(event.target.value == "desc"){
                this.countries.sort((a,b)=>b.name.official.localeCompare(a.name.official));
                this.$emit('update:tempCountries',this.countries);
                
            }
            else{
                this.$emit('update:tempCountries',this.countriesData);
                
            }
            this.displayCountry();
        },
    }
}
</script>
<style lang="">
    
</style>