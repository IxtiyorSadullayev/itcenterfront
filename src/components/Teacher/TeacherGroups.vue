<script>
export default {
    name:'teachergroups',
}
</script>

<template>
    <h4>O'qiyotgan va tugatgan o'quv kurslari ro'yxati.</h4>
    <div class="groups">
        <div class="group">
            <h1>Guruh nomi</h1>
            <p>O'quvchilari soni.</p>
            <p>O'qiyotgan kurs nomi </p>
            <p>Nechta dars o'tganligi </p>
            <p>Guruh ijtimoiy tarmoqlari ro'yxati </p>
        </div>
        
    </div>
</template>

<style scoped>
    .groups{
        width: 100%;
        min-height: 100px;
        display: flex;
        align-items: center;
        justify-content: safe;
        flex-wrap: wrap;
    }
    .group{
        width: 300px;
        min-height: 300px;
        background-color: yellow;
        margin: 5px;
        border: 1px solid transparent;
        box-shadow: 0 2px 4px black;
    }
</style>