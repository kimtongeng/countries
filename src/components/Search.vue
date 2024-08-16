<template>
    <form class="d-flex">
        <input class="form-control me-2" type="search" placeholder="Search" v-model="search" aria-label="Search">   
    </form>
</template>
<script>
import Fuse from 'fuse.js'
export default {
    props:["countriesData","countries",'displayCountry'],
    data(){
        return {
            search:""
        }
    },
    watch: {
        search(newVal,oldVal){
            if(newVal != ""){
                const fuse = new Fuse(this.countriesData, { keys: ["name.official","name.common"] });
                this.$emit("update:countries",fuse.search(newVal).map((value)=>value.item));
            }
            else{
                this.$emit("update:countries",this.countriesData);
                this.displayCountry();
            }
        },
    },
}
</script>
<style lang="">
    
</style>