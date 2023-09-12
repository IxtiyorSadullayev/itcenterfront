<script>
import axios from 'axios';
import UpdateStudent from '../components/Student/UpdateStudent.vue';

export default{
    name: 'student_view',
    created() {
        this.getStudent();
    },
    data() {
        return {
            student: {},
            update: 'bosh'
        };
    },
    methods: {
        async getStudent() {
            await axios.get('http://localhost:5000/api/student/' + this.$route.params.id)
                .then(res => {
                // console.table(res.data)
                this.student = res.data;
            })
                .catch(err => {
                console.log(err.message);
            });
        },
        updateAction() {
            this.update = 'update';
        },
        ortgaAction(){
            this.update = 'bosh'
        }
    },
    components: { UpdateStudent }
}
</script>

<template>
    <div class="container">
        <div class="student">
            <h1>
                {{ student.fullname }}  {{ student.surname }}  {{ student.fathername }}
                
            </h1>
            <div class="wrapper" v-if="update == 'bosh'">
                <div class="passport">
                    <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSgBhcplevwUKGRs1P-Ps8Mwf2wOwnW_R_JIA&usqp=CAU" alt="rasm">
                    <p><span>{{ student.passportseria }}</span> <span>{{ student.passportnumber }}</span></p>
                </div>
                <p>Tug'ilgan kuni:  <span>{{ student.birthday }}</span></p>
                <p>Telefon raqami:  <span>{{ student.phone }}</span></p>
                <p>Guruh nomi: <span>{{ student.group.tagname || ''}}</span></p>
                <p>Davomiyligi:  <span>{{ student.group.group_along }}</span></p>
                <p>Guruh raqami:  <span>{{ student.group.group_number }}</span></p>
                <p>Boshlangan sanasi: <span>{{ student.group.createdAt.split('T')[0] }}</span></p>
                <p>Jinsi: <span>{{ student.gender }}</span></p>
                <p>Status: {{ student.status|| "O'qimoqda" }}</p>
                <div class="btns">
                    <button @click="updateAction">O'zgartirish</button>
                    <button>O'chirish</button>
                </div>
            </div>
            <div class="wrapper" v-if="update == 'update'">
                <UpdateStudent @bosh="ortgaAction"  :student="student"/>
            </div>
        </div>
    </div>
</template>

<style scoped>
h1{
    font-family: 'Courier New', Courier, monospace;
}
.container {
    width: 80%;
    height: 100%;
    display: block;
    margin: 0 auto 10px auto;
    background-color: rgba(179, 179, 174, 0.164);
    padding: 10px;
}

.student {
    width: 100%;
    min-height: 100px;
    background-color: white;
    border-radius: .6rem;
    padding: 10px;
}
.wrapper{
    min-height: 100px;
    width: 100%;
    position: relative;
}
.wrapper p{
    font-size: 16px;
    font-weight: bold;
    font-family: 'Courier New', Courier, monospace;
    word-spacing: 5px;
    letter-spacing: 2px;
}
.passport p{
    position: absolute;
    top: 0;
    right: 200px;
    font-size: 40px;
    font-family: 'Courier New', Courier, monospace;
}
.btns{
    position: absolute;
    bottom: 0;
    right: 100px;
}
.btns button{
    display: block;
    margin: 10px;
    font-size: 16px;
    font-weight: bold;
    font-family: 'Courier New', Courier, monospace;
    padding: 5px;
    text-transform: uppercase;
}
</style>