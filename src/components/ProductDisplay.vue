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
        }
    },

    mounted() {
        this.fetchData();
    },

    methods:{
        fetchData() {
            fetch('https://fakestoreapi.com/products')
            .then(response => response.json())
            .then(data => {
                this.products = data;
            })
            .catch(error => {
                console.error('Error:', error);
            });
        },

        nextTitle() {
            this.currentIndex++;
            this.updateCurrentTitle();
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
        }

        

    },
}
</script>


<template>
    <div>
        <div class="container">
            <div class="back1" :style="{ backgroundColor: currentCategoryColor }"></div>
            <div class="card">
                <div class="img" v-if="currentCategory === 'men\'s clothing' || currentCategory === 'women\'s clothing'">
                    <img :src="currentImage" alt="Product Image">
                </div>
                <div class="detail">
                    <div class="title" v-if="currentCategory === 'men\'s clothing' || currentCategory === 'women\'s clothing'" :style="{ color: titleColor }"> {{ currentTitle }}</div>
                    <div class="category" v-if="currentCategory === 'men\'s clothing' || currentCategory === 'women\'s clothing'">{{ currentCategory }}</div>
                    <div class="description" v-if="currentCategory === 'men\'s clothing' || currentCategory === 'women\'s clothing'">{{ currentDescription }}</div>
                    <div class="price" v-if="currentCategory === 'men\'s clothing' || currentCategory === 'women\'s clothing'" :style="{ color: titleColor }">{{ currentPrice }}</div>
                    <div class="button">
                        <button v-if="currentCategory === 'men\'s clothing' || currentCategory === 'women\'s clothing'">Buy</button>
                        <button @click="nextTitle">Next</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    
</template>


<style>
@import "../assets/style.css";
</style>


