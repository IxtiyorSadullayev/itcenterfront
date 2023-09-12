<script>
import axios from 'axios'
import Teacher from '../components/Teacher.vue';

export default {
    name: 'teachers',
    components: { Teacher },
    created(){
        this.getTeacherType()
        this.getTeachers()
    },
    data() {
        return {
            fullname: '',
            surname: '',
            birthday: '',
            teacher_type: '',
            order: '',
            rate: '',
            teachers: [],
            types: []
        }
    },
    methods: {
       async addNewTeacher() {
            await axios.post('http://localhost:5000/api/teacher/add', {
                fullname: this.fullname,
                surname: this.surname,
                birthday: this.birthday,
                teacher_type: this.teacher_type,
                order: this.order,
                rate: this.rate,
            })
                .then(res =>{
                    this.getTeachers();                    
                })
                .catch(err=>{
                    console.log(err.message)
                })
        },
        async getTeacherType(){
            await axios.get('http://localhost:5000/api/teacher/type/getall')
                .then(res => {
                    this.types=res.data;
                })
                .catch(err=>{
                    console.log(err.message)
                })
        },
        async getTeachers(){
            await axios.get('http://localhost:5000/api/teacher/all')
                .then(res => {
                    this.teachers=res.data;
                })
                .catch(err=>{
                    console.log(err.message)
                })
        }
        
    }
}

</script>

<template>
    <div class="container">
        <div class="addteacher">
            <h3>Yangi ishchi qo'shish</h3>
            <input type="text" v-model="fullname" placeholder="Familiya...">
            <input type="text" v-model="surname" placeholder="Ism...">
            <input type="date" v-model="birthday" placeholder="Tug'ilgan yil...">
            <select name="type" v-model="teacher_type" id="type">
                <option value="">Ishchi turi</option>
                <option v-for="type in types"  :value="type._id">{{ type.teacher_type }}</option>
            </select>
            <input type="text" v-model="order" placeholder="Buyruq raqami...">
            <input type="text" v-model="rate" placeholder="Stavkasi...">
            <button @click="addNewTeacher">Qo'shish</button>
            <button>Qidirish</button>
        </div>

        <div class="teachers">
            <h3>Ishchilar ro'yxati</h3>
            <table id="teachers">
                <thead>
                    <tr>
                        <th id="uuid">
                            №
                        </th>
                        <th id="fio">
                            FIO
                        </th>
                        <th id="birth_day">
                            Tug'ilgan kuni
                        </th>
                        <th id="actions">
                            Harakatlar
                        </th>
                    </tr>
                </thead>
                <tbody>

                    <Teacher v-for="teacher in teachers" :tartib="teacher.tr" :fam="teacher.fullname" :name="teacher.surname" :birth_day="teacher.birthday">
                        <RouterLink :to="`/teacher/${teacher.id}`">...</RouterLink>
                    </Teacher>
                </tbody>
            </table>
        </div>

    </div>
</template>


<style scoped>
.container {
    width: 80%;
    height: 100%;
    display: block;
    margin: 0 auto 10px auto;
    background-color: rgba(179, 179, 174, 0.164);
    padding: 10px;
}

.addteacher {
    width: 100%;
    min-height: 100px;
    background-color: white;
    border-radius: .6rem;
    padding: 10px;
}

.addteacher input,
select,
option,
button {
    height: 40px;
    margin: 0 5px;
}

button {
    margin-top: 5px;
    padding: 0 20px;
}

.teachers {
    margin-top: 20px;
    width: 100%;
    min-height: 100px;
    background-color: white;
    border-radius: .6rem;
    padding: 10px;
}

#teachers {
    border-collapse: collapse;
    width: 100%;
}

#teachers thead {
    text-align: left;
}

tbody {
    width: 100%;
}

#teachers,
th,
td {
    border: 1px solid black;
    color: black;
    font-weight: bold;
    background-color: rgba(128, 128, 128, 0.288);
    padding: 5px;
}

#uuid {
    width: 5%;
}

#fio {
    width: 40%;
}

#birth_day {
    width: 30%;
}</style>