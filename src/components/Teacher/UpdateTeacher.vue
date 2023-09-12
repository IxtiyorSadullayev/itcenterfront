<script>
import axios from 'axios'
export default {
    name: 'updateteacher',
    props: {
        teacher: Object,
        teacher_id: String
    },
    created() {
        this.surname = this.teacher.surname;
        this.fullname = this.teacher.fullname;
        this.birthday = this.teacher.birthday;

    },
    data() {
        return {
            surname: '',
            fullname: '',
            birthday: '',
            order: '',
            rate: '',
        }
    },
    methods: {
        async updateUser(){
            this.$emit('updateUser', this.surname, this.fullname, this.birthday)
        }
    }
}
</script>
<template>
    <div>
        <label for="surname">O'qituvchi ismi: </label>
        <input type="text" id="surname" v-model="surname" placeholder="Ism ...">
    </div>
    <div>
        <label for="fullname">O'qituvchi familiyasi: </label>
        <input type="text" id="fullname" v-model="fullname" placeholder="Familiyasi ...">
    </div>
    <div>
        <label for="birthday">O'qituvchi tug'ilgan kuni: {{ teacher.birthday }} </label>
        <input type="date" id="birthday" v-model="birthday">
    </div>
    <div>
        <label for="order">O'qituvchi stavkasi</label>
        <input type="text" id="order" placeholder="Buyruq raqami ..." disabled :value="teacher.order">
    </div>
    <div>
        <label for="rate">O'qituvchi stavkasi</label>
        <input type="text" id="rate" placeholder="Stavkasi ..." disabled :value="teacher.rate">
    </div>
    <button @click="updateUser()">Saqlash</button>
</template>
<style scoped></style>