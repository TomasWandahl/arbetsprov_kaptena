<template>
    <div class="company-wrapper">
        <div class="company">
        <h2 class="company-name">{{company.companyName}}</h2>
          <p>Organisationsnummer: {{company.companyId}}</p>
          <p>{{company.visitAddress}} <br /> {{company.zipCode}} {{company.city}}</p>
          <div class="employees-wrapper">
            <h3 class="employees-title">Anställda</h3>
            <div class="employees">
              <div v-for ="role in company.roles" :key="role.personalNumber" class="employee">
                  <Employee :role = role.role :personalNumber = role.personalNumber :getPersonName =  getPersonName />
              </div>
            </div>       
          </div>
    </div>
    </div>
</template>
<script>
    import Employee from './Employee';

    export default {
        props: ['company', 'persons', 'getPersonName'],
        components : {
            Employee
        }
    }
</script>

<style>
    .company-wrapper {
        border-radius: 5px;
        margin: 20px;
        background-color: rgba(255, 255, 255, 0.95);
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
    .employee {
        background-color: rgba(18, 104, 90, 0.8);
        color: #fff;
        padding: 5px;
        width: 45%;
        margin-top: 10px;
        text-align: center;
        border-radius: 5px;
    }
    .employees-title {
        margin: 20px 0;
        text-align: center;
        font-size: 25px;
    }
</style>

