<template>
    <form class="search-form" @submit.prevent="getCompany(searchQuery)">
        <input placeholder="Sök på ett företag" autocomplete="off" class="search-bar" type="text" name="searchCompany" id="searchCompany" v-model="searchQuery">
        <button type="reset" @click="showAllCompanies">Visa alla företag</button>
        <button type="submit">Sök</button>
    </form>
</template>

<script>
export default {
    props: ['getCompany', 'showAllCompanies'],
    data () {
        return {
            searchQuery: '',
        }
    }
}
</script>

<style>
    .search-form {
        display:flex;
        justify-content: center;
        flex-wrap: wrap;
        width: 44%;
        margin: 0 auto;
        
    }

    .search-form button {
        height: 50px;
        padding: 5px;
        width: 125px;
        margin: 20px 10px 20px 10px;
        border: none;
        border-radius: 4px;
        box-shadow: 1px 3px rgba(0,0,0, 0.30);
        font-size: 15px;
        font-weight: bold;
        font-family: 'montserrat', sans-serif;
        color: #3b5166;
        cursor: pointer;
    }

    .search-bar {
        width: 100%;
        height: 50px;
        padding: 20px;
        border: none;
        appearance: none;
        font-size: 20px;
        box-shadow: 1px 3px rgba(0,0,0, 0.30);
    }

    @media screen and (max-width: 800px) {
        .search-form {
            width: 80%;
        } 
    }
</style>