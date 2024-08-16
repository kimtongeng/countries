<template >
     <nav aria-label="">
        <ul class="pagination">
            <li class="page-item">
                <button @click="handlePerv" v-if="currentPage > 1" class="page-link">perv</button>
            </li>
            <li class="page-item" :class="{'active': currentPage == page}" v-for="page in pagesShow" @click="handlePageChange(page)"><button class="page-link">{{ page }}</button></li>
            <li class="page-item">
                <button @click="handleNext" v-if="currentPage < 10" class="page-link">next</button>
            </li>   
        </ul>
    </nav>
</template>
<script>
export default {
    props:['pagesShow','currentPage','itemsPerPage','displayCountry'],
    methods:{
        handlePerv(){
            this.$emit("update:currentPage",this.currentPage-1);
            this.displayCountry();
        },
        handleNext(){               
            this.$emit("update:currentPage",this.currentPage+1);
            this.displayCountry();

        },
        handlePageChange(page){
            this.$emit("update:currentPage",page);
            this.displayCountry();
        },
    },
    
}
</script>
<style lang="">
    
</style>