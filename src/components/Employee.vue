<template>
    <div>
        <p class="employee-title">{{role}}</p>
        <p class="employee-name">{{getPersonName(personalNumber)}}</p>
    </div>
</template>

<script>
export default {
    props: ['role', 'personalNumber', 'getPersonName'],
}
</script>

<style>
    .employee-title {
        text-transform:capitalize;
        font-weight: 700;
        font-size: 18px;
    }
</style>