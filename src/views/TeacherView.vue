<script>
import axios from 'axios';
import Hodim from '../components/Hodim.vue';
import TeacherAccount from '../components/Teacher/TeacherAccount.vue';
import TeacherGroups from '../components/Teacher/TeacherGroups.vue';
import UpdateTeacher from '../components/Teacher/UpdateTeacher.vue';

export default{
    name: 'teacher',
    created() {
        this.teacherId = this.$route.params.id;
        this.getTeacher();
    },
    data() {
        return {
            teacherId: '',
            teacher: '', 
            manzil: 'home'
        };
    },
    methods: {
        async getTeacher() {
            await axios.get('http://localhost:5000/api/teacher/get/' + this.teacherId)
                .then(res => {
                this.teacher = res.data;
                console.log(res.data);
            })
                .catch(err => {
                console.log(err.message);
            });
        },
        async updateUser(surname, fullname, birthday){
            await axios.patch('http://localhost:5000/api/teacher/update/'+this.teacherId, {
                surname: surname, fullname: fullname, birthday: birthday
            })
                .then(res => {
                    this.getTeacher()                    
                })
                .catch(err =>{
                    console.log(err.message)
                })
        }
    },
    components: { Hodim, UpdateTeacher, TeacherGroups, TeacherAccount }
}
</script>
<template>
    <div class="container">
        <div class="teacher">
            <h3>Hodim: {{ teacher.fullname }} {{ teacher.surname }}</h3>
            <ul class="teacher_links">
                <li @click="()=> manzil = 'home'">Ma'lumotlar</li>
                <li @click="()=> manzil = 'tahrir'">Tahrirlash</li>
                <li @click="()=> manzil = 'guruhlar'">O'quvchilari soni va guruhlari</li>
                <li @click="()=> manzil = 'login'">Login va paroli.</li>
            </ul>
            <Hodim v-if="manzil == 'home'" :teacher="teacher" />
            <UpdateTeacher v-else-if="manzil == 'tahrir'" :teacher_id="teacher.id" :teacher="teacher" @updateUser="updateUser" />
            <TeacherGroups v-else-if="manzil == 'guruhlar'" />
            <TeacherAccount v-else-if="manzil == 'login'" />
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

.teacher {
    width: 100%;
    min-height: 100px;
    background-color: white;
    border-radius: .6rem;
    padding: 10px;
}
.teacher_links{
    width: 100%;
    height: auto;
    display: flex;
    align-items: center;
    justify-content: flex-start;
    list-style-type: none;
}
.teacher_links li{
margin: 0 5px;
border: 1px solid transparent;
}
.teacher_links li:hover{
    border-bottom: 1px solid blue;
    cursor: pointer;
}
</style>