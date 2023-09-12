<script>
import {RouterLink} from 'vue-router'
export default {
    name: 'student',
    props: ['tartib', 'fam', 'ism', 'father', 'birthday', 'group', '_id'],
}
</script>
<template>
    <tr>
        <td class="uuid">{{ tartib }}</td>
        <td class="fam">{{ fam }}</td>
        <td class="name">{{ ism }}</td>
        <td class="fatder">{{ father }}</td>
        <td class="birtd_day">{{ birthday }}</td>
        <td class="group">{{ group }}</td>
        <td>
            <RouterLink :to="`/student/${_id}`">...</RouterLink>
        </td>
    </tr>
</template>

<style scoped>
td {
    border: 1px solid black;
}

img {
    width: 30px;
}
</style>