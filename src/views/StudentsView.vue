<script>
import axios from 'axios';
import Student from '../components/Student.vue';
export default {
    name: 'students',
    components: { Student },
    created() {
        this.getGroupsList()
        this.getAllStudents()
    },
    data() {
        return {
            fullname: '',
            surname: '',
            fathername: '',
            passport_seria: '',
            passport_number: '',
            phone: "",
            birth_day: '',
            gender: '',
            group: '',
            groups: [],
            teacher_type: [],
            students: []
        }
    }, 
    methods:{
        async addstudent (){
            await axios.post('http://localhost:5000/api/student/add', {
                fullname: this.fullname,
                surname: this.surname,
                fathername: this.fathername,
                passportseria: this.passport_seria,
                passportnumber: this.passport_number,
                birthday: this.birth_day,
                phone:this.phone,
                gender: this.gender,
                group: this.group
            })  
                .then(res =>{
                    // console.log(res
                    this.fullname = ''
                    this.surname = ''
                    this.fathername = ''
                    this.passport_number = ''
                    this.passport_seria = ''
                    this.birth_day = ''
                    this.phone = ''
                    this.gender = ''
                    this.group = ''
                    this.getAllStudents()
                })
                .catch(err =>{
                    console.log(err.message)
                })
        },
        async getGroupsList(){
            await axios.get('http://localhost:5000/api/group/all')
                .then(res =>{
                    this.groups = res.data;
                })
                .catch(err=>{
                    console.log(err.message)
                })
        },
        async getAllStudents(){
            await axios.get('http://localhost:5000/api/student/all')
                .then(res =>{
                    this.students = res.data;
                })
                .catch(err =>{
                    console.log(err.message)
                })
        }
    }
}
</script>

<template>
    <div class="container">
        <div class="addstudent">
            <h3>O'quvchi ma'lumotlarini kiriting</h3>
            <input type="text" v-model="fullname" placeholder="Familiyasi ...">
            <input type="text" v-model="surname" placeholder="Ismi ...">
            <input type="text" v-model="fathername" placeholder="Otasining ismi ...">
            <input type="text" v-model="passport_seria" placeholder="Passport seria">
            <input type="text" v-model="passport_number" placeholder="Passport raqam">
            <input type="tel" v-model="phone" placeholder="Telefon raqami...">
            <input type="date" v-model="birth_day">
            <select name="jins" id="jins" v-model="gender">
                <option value="">Jinsi</option>
                <option value="Erkak">Erkak</option>
                <option value="Ayol">Ayol</option>
            </select>
            <select name="uquv_guruhi" id="uquv_guruhi" v-model="group" >
                <option value="">O'quv guruhi</option>
                <option v-for="gr in groups" :value="gr._id">{{ gr.tagname }}</option>
            </select>
            <button @click="addstudent">Saqlash</button>
            <button>Qidirish</button>
        </div>
        <div class="addstudent">
            <table id="uquvchilar">
                <thead>
                    <tr>
                        <th class="uuid">№</th>
                        <th class="fam">Familiya</th>
                        <th class="name">Ism</th>
                        <th class="father">Otasining ismi</th>
                        <th class="birth_day">Tug'ilgan sanasi</th>
                        <th class="group">Guruhi</th>
                        <th class="group">Actions</th>
                    </tr>
                </thead>
                <tbody>
                    <Student v-for="st in students" 
                    :tartib="st.id"
                    :fam="st.fullname"
                    :ism="st.surname"
                    :father="st.fathername"
                    :birthday="st.birthday"
                    :group="st.group"
                    :_id ="st._id"
                    />
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

.addstudent {
    width: 100%;
    min-height: 100px;
    background-color: white;
    border-radius: .6rem;
    padding: 10px;
    margin-bottom: 10px;
}

.addstudent input,
select,
button {
    height: 40px;
    padding: 5px;
    margin: 5px 5px;
}

#uquvchilar {
    border-collapse: collapse;
    width: 100%;
}

#uquvchilar tr,
th,
td {
    border: 1px solid black;
}

#uquvchilar th {
    font-weight: bold;
    background-color: rgb(170, 218, 218);
}

#uquvchilar thead {
    width: 100%;
}

.uuid {
    min-width: 3%;
}

.fam {
    width: 20%;
}

.name {
    width: 20%;
}

.father {
    width: 20%;
}

.birth_day {
    width: 15%;
}</style>