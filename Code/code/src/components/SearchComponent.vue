<template>
    <div>
      
      <!-- Search bar (commented out) -->
      <div class="search-bar" :class="{ active: searchBarActive }" @click="toggleSearchBar">
        <input type="text" placeholder="Search..." class="search-input" v-model="searchText" @input="onSearch" />
        <div v-if="searchText || searchBarActive" class="clear-text" @click.stop="clearText">Clear</div>
      </div>
  
      <!-- Display search results as div elements -->
      <div class="search-results" v-if="searchValues?.length > 0">
        <div v-for="(searchValue, index) in searchValues" :key="index" class="result-item">
            <div v-if="searchValue?.productId !== null" > 
                <ProductView :productId="searchValue?.productId" ></ProductView>
                <!-- {{ searchValue }} -->
            </div>
            <!-- <div v-if="searchValue?.productId !=null" @click="routeToQn(questionId,searchValue.searchTerm)">{{ searchValue.searchTerm }}</div> -->
        </div>
      </div>
      <div v-else>
        No results found.
      </div>
    </div>
  </template>
  
  <script>
import { ref, computed } from 'vue';
import useSearchStore from '@/store/search-store';
import ProductView from './ProductView.vue';
// import router from '../router/index.js';
// import { useProductStore } from '../store/product-store.js';
  // import debounce from 'lodash.debounce';

  export default {
    setup() {
        const searchBarActive = ref(false);
        const searchText = ref('');
        const searchStore = useSearchStore();
        // const productStore = useProductStore()
        // searchStore.FETCH_Search();
        const searchValues = computed(() => {
            return searchStore.searchData;
        });

      //   const routeToQn = (questionId,questionName) => {
      //     answerStore.updateQuestionInfo( questionId,);
      // answerStore.updateQuestionName(questionName );
    
      // router.push("/questioninfopage"); 
      //   }
        return {
            searchBarActive,
            searchText,
            searchValues,
            // routeToQn
        };
    },
    components: { ProductView }
};
  </script>
  
  <style scoped>
  .search {
    margin-top: 90px;
  }
  
  /* Styles for the search results */
  .search-results {
    margin-top: 100px;
    display: flex;
    flex-wrap: wrap;
    align-content: stretch;
    flex-direction: column;
   align-items: center;
  }
  
  .result-item {
    border: 1px solid;
    margin: 10px;
    padding: 10px;
    width: 700px; /* Adjust the width as needed */
  }
  
  /* Add more styles based on your design preferences */
  </style>
  