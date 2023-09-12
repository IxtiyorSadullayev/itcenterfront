<script>
export default {
    name: 'hodim',
    created(){

    },
    props:['teacher']
}
</script>

<template>
<p>Ismi : {{ teacher.surname }}</p>
<p>Otasining ismi : {{ teacher.fullname }}</p>
<p>Tug'ilgan kuni : {{ teacher.birthday }}</p>
<p>O'qituvchi turi : {{ teacher.teacher_type.teacher_type }}</p>
<p>Buyruq raqami : {{ teacher.order }}</p>
<p>Hodim stavkasi : {{ teacher.rate }}</p>
</template>

<style scoped>

</style>