<template>
  <div id="app">
    <h1 class="title"> Arbetsprov </h1>
    <div class="companies">
        <div v-for="company in companies" :key="company.companyId" class="company-wrapper">
          <h2 class="company-name">{{company.companyName}}</h2>
          <p>Organisationsnummer: {{company.companyId}}</p>
          <p>{{company.visitAddress}} <br /> {{company.zipCode}} {{company.city}}</p>
          <div class="employees-wrapper">
            <h3 class="employees-title">Anställda</h3>
            <div class="employees">
              <div v-for ="role in company.roles" :key="role.personalNumber" class="employee">
                <p class="employee-title">{{role.role}}</p>
                <p class="employee-name">{{getPersonName(role.personalNumber)}}</p>
              </div>
            </div>
              
          </div>
        </div>
        
    </div>
  </div>
</template>
<script>


export default {
  name: 'App',
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

      let person = this.getPersonData('196202015530');
      console.log(person.firstName);
    },

    async fetchData(url) {
      const companies = await fetch(url);
      const companiesJSON = await companies.json();
      return companiesJSON;
    },

    getPersonName(pnum) {
      let person = this.persons.filter(x => x.personalNumber == pnum)[0];
      return `${person.firstName} ${person.surName}`;
    },

    getNumber() {
      return 123;
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
  background-color: #8BC6EC;
  background-color: #8BC6EC;
  background-image: linear-gradient(285deg, #8BC6EC 0%, #9599E2 100%);
}

.hide {
  display: none;
}

#app {
  font-family: 'montserrat', sans-serif;
  color: #3b5166;
  margin-top: 60px;
}

.title {
  text-align: center;
  font-size: 52px;
  font-weight: 500;
  text-shadow: 0;
  text-shadow: 1px 3px rgba(0,0,0, 0.20);
  color: #fff;
}

.companies {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}

.company-wrapper {
  border-radius: 5px;
  margin: 20px;
  background-color: rgba(255, 255, 255, 0.45);
  box-shadow: 1px 3px rgba(0,0,0,0.15);
  padding: 20px;
  width: 400px;
}

.company-wrapper p {
  margin: 10px 0;
}

.employees {
  display: flex;
  flex-wrap: wrap;
  justify-content:space-evenly;

}

.employees-title {
  margin: 20px 0;
  text-align: center;
  font-size: 25px;
}

.employee {
  background-color: rgba(255, 255, 255, 0.75);
  padding: 5px;
  width: 45%;
  margin-top: 10px;
  text-align: center;
  border-radius: 5px;
}

.employee-title {
  text-transform:capitalize;
  font-weight: 700;
  font-size: 18px;
}

</style>
