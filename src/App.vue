<template>
  <div id="app">
    <div class="bg-image"></div>
    <h1 class="title"> Arbetsprov </h1>
    <div class="companies">
        <div v-for="company in companies" :key="company.companyId">
            <Company :company = company :getPersonName =  "getPersonName" />
        </div>
    </div>
  </div>
</template>
<script>

import Company from './components/Company';

export default {
  name: 'App',
  components: {
    Company
  },
  data () {
    return {
      message: 'message',
      companies: {},
      persons: {}
    }
  },
  beforeMount() {
    this.setData();
  },
  methods: {
    async setData() {
      this.companies = await this.fetchData("https://cors-anywhere.herokuapp.com/kap-csd.herokuapp.com/api/assessment/companies");
      this.persons = await this.fetchData('https://cors-anywhere.herokuapp.com/kap-csd.herokuapp.com/api/assessment/persons');
    },

    async fetchData(url) {
      const companies = await fetch(url);
      const companiesJSON = await companies.json();
      return companiesJSON;
    },
    getPersonName(pnum) {
      let person = this.persons.filter(x => x.personalNumber == pnum)[0];
      return `${person.firstName} ${person.surName}`;
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  
}

.bg-image {
  background-image: url('./assets/bg.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;

  position: absolute;
  left: 0;
  top: 0;
  width: 100vw;
  height: 100vh;

  z-index: -1;
  filter: blur(5px);
}

#app {
  font-family: 'montserrat', sans-serif;
  color: #3b5166;
}

.title {
  text-align: center;
  font-size: 52px;
  font-weight: 500;
  text-shadow: 0;
  text-shadow: 1px 3px rgba(0,0,0, 0.20);
  color: #fff;
  background-color: #12685A;
  padding: 15px;
  margin-bottom: 20px;
}
.companies {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
</style>
