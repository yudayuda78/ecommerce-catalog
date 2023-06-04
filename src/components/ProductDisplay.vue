<script>
export default{
    // name: ProductDisplay,
    data() {
        return{
            products : [],
            currentIndex: 0,
            currentTitle: '',
            currentCategory: '',
            currentDescription: '',
            currentPrice: '',
            currentImage: '',
            currentCategoryColor: '',
            titleColor: '',
            isLoading: false,
        }
    },

    mounted() {
        this.fetchData();
        this.updateCurrentTitle()
    },

    methods:{
        fetchData() {
            this.isLoading = true;
            fetch('https://fakestoreapi.com/products')
            .then(response => response.json())
            .then(data => {
                this.products = data;
                this.currentIndex = 0;
                this.updateCurrentTitle();
                this.isLoading = false;
            })
            .catch(error => {
                console.error('Error:', error);
                this.isLoading = false;
            });
        },

        nextTitle() {
            this.isLoading = true;
            this.currentIndex++;
            this.updateCurrentTitle();
            setTimeout(() => {
                this.updateCurrentTitle();
                this.isLoading = false;
            }, 1000);
        },

        updateCurrentTitle() {
            if (this.currentIndex >= this.products.length) {
            this.currentIndex = 0;
            }
            this.currentTitle = this.products[this.currentIndex].title;
            this.currentCategory = this.products[this.currentIndex].category;
            this.currentDescription = this.products[this.currentIndex].description;
            this.currentPrice = this.products[this.currentIndex].price;
            this.currentImage = this.products[this.currentIndex].image;

            if (this.currentCategory === "men's clothing") {
                this.currentCategoryColor = '#D6E6FF';
                this.titleColor = '#002772';
            } else if (this.currentCategory === "women's clothing") {
                this.currentCategoryColor = '#FDE2FF';
                this.titleColor = '#720060';
            } else{
                this.currentCategoryColor = '#DCDCDC';
                this.titleColor = '';
            }



        },



        

    },
}
</script>


<template>
    <div>
        <div class="container">
            <div v-if="isLoading" class="loading">Loading...</div>
            <div class="back1" :style="{ backgroundColor: currentCategoryColor }"></div>
            <div class="card">
                <div class="img" v-if="currentCategory === 'men\'s clothing' || currentCategory === 'women\'s clothing'">
                    <img :src="currentImage" alt="Product Image">
                </div>
                <div class="detail">
                    <div class="title" v-if="currentCategory === 'men\'s clothing' || currentCategory === 'women\'s clothing'" :style="{ color: titleColor }"> {{ isLoading ? 'Loading...' : currentTitle }}</div>
                    <div class="category" v-if="currentCategory === 'men\'s clothing' || currentCategory === 'women\'s clothing'">{{ currentCategory }}</div>
                    <div class="description" v-if="currentCategory === 'men\'s clothing' || currentCategory === 'women\'s clothing'">{{ currentDescription }}</div>
                    <div class="price" v-if="currentCategory === 'men\'s clothing' || currentCategory === 'women\'s clothing'" :style="{ color: titleColor }">${{ currentPrice }}</div>
                    <div class="aware" v-if="!(currentCategory === 'men\'s clothing' || currentCategory === 'women\'s clothing')" >{{ isLoading ? 'Loading...' : 'This product is unavailable to show' }}</div>
                    <div class="button">
                        <button class="category-button" v-if="currentCategory === 'men\'s clothing' || currentCategory === 'women\'s clothing'" :style="{ borderColor: titleColor }">Buy</button>
                        <button class="category-button" v-if="currentCategory === 'men\'s clothing' || currentCategory === 'women\'s clothing'" @click="nextTitle" :style="{ borderColor: titleColor }">Next</button>
                        <button class="category-button second-button" v-if="!(currentCategory === 'men\'s clothing' || currentCategory === 'women\'s clothing')" @click="nextTitle" :style="{ borderColor: titleColor}">Next</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    
</template>


<style>
@import "../assets/style.css";
</style>


