<script>
export default {
    name: 'teacher',
    props:['tartib', 'fam', 'name',  'birth_day']
}
</script>

<template>
    <tr>
        <td class="tr">
            {{ tartib }}
        </td>
        <td class="fio">
            {{ fam }} {{ name }}
        </td>
        <td class="birth_day">
            {{ birth_day }}
        </td>
        <td class="actions">
            <slot></slot>
        </td>
    </tr>
</template>

<style scoped>
tr{
    width: 100%!important;
}
tr,td{
    padding: 5px;
    border: 1px solid black;
    text-align: left;
    border-collapse: collapse;
    background-color: white;
}
.tr{
    width: 5%;
}
.fio{
    width: 40%;
}
.birth_day{
    width: 30%;
}
.actions{
    width: 25%;
}
</style>