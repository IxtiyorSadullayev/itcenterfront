<script>
import axios from 'axios';

export default {
    name: 'updatestudent',
    props:{
        student:{
            type: Object,
            requred: true
        }
    },emits: ['bosh'],
    created(){
        this.getdataProps()
    },  
    data(){
        return{
            surname: '',
            fullname: '',
            fathername: '',
            birthday: '',
            group: '',
            status: '',
            phone: '',
            gender: '',
            passportseria: '',
            passportnumber: '',
        }
    },
    methods:{
        getdataProps(){
            this.surname = this.student.surname;
            this.fullname = this.student.fullname;
            this.fathername = this.student.fathername;
            this.birthday = new Date(this.student.birthday).toISOString().split('T')[0];
            this.group = this.student.group;
            this.phone = this.student.phone;
            this.gender = this.student.gender;
            this.passportseria = this.student.passportseria;
            this.passportnumber = this.student.passportnumber;
        },
        boshstudent(){
            this.$emit('bosh')
        },
        async updateStudent(){
            await axios.patch()
        }
    }
}
</script>

<template>
    <div class="inputgroup">
        <label for="fullname">Familiyasi: </label>
        <input type="text" id="fullname" v-model="fullname" placeholder="Familiya ...">
    </div>
    <div class="inputgroup">
        <label for="surname">Ism: </label>
        <input type="text" id="surname" v-model="surname" placeholder="Ism ...">
    </div>
    <div class="inputgroup">
        <label for="fathername">Otasining ismi: </label>
        <input type="text" id="fathername" v-model="fathername" placeholder="Otasining ismi ...">
    </div>
    <div class="inputgroup">
        <label for="birthday">Tug'ilgan kuni: </label>
        <input type="date" v-model="birthday" id="birthday" >
    </div>
    <div class="inputgroup">
        <label for="passportseria">Passport seria: </label>
        <input type="text" v-model="passportseria" id="passportseria" >
    </div>
    <div class="inputgroup">
        <label for="passportnumber">Passport number: </label>
        <input type="text" v-model="passportnumber" id="passportnumber" >
    </div>
    <div class="inputgroup">
        <label for="status">Statusi: </label>
        <select name="status" id="status">
            <option >Status</option>
            <option value="O'qimoqda">O'qimoqda</option>
            <option value="Bitirgan">Bitirgan</option>
            <option value="Ketgan">Ketgan</option>
        </select>
    </div>
    <div class="btns">
        <button @click="boshstudent">Ortga</button>
        <button>Saqlash</button>
    </div>
</template>
<style scoped>
    .inputgroup{
        display: grid;
        margin: 0 5px;
        gap: 5px;

    }
    .inputgroup input, select{
        height: 30px;
        padding: 5px;
        font-family: 'Courier New', Courier, monospace;
        margin-bottom: 5px;
    }
    .inputgroup label{
        font-family: 'Courier New', Courier, monospace;
        font-size: 16px;
    }
    .btns button{
        margin: 0 5px;
        height: 30px;
        font-family: 'Courier New', Courier, monospace;
        font-weight: bold;
    }
</style>