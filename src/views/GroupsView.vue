<script>
import axios from 'axios'
export default {
    name: 'groups',
    created(){
        this.getCoursesList();
        this.getTeachersList();
        this.getGroups()
    },
    data(){
        return {
            groupname: '',
            tagname: '',
            started: '',
            group_number: '',
            group_along: '',
            teacher: '',
            courses: [],
            teachers: [],
            groups:[]
        }
    },
    methods:{
        async getCoursesList(){
            await axios.get('http://localhost:5000/api/kurs/type/all')
                .then(res=>{
                    this.courses = res.data;
                })
                .catch(err=>{
                    console.log(err.message)
                })
        },
        async getTeachersList(){
            await axios.get('http://localhost:5000/api/teacher/all')
                .then(res =>{
                    this.teachers = res.data;
                })
                .catch(err=>{
                    console.log(err.message)
                })
        },
        async getGroups(){
            await axios.get('http://localhost:5000/api/group/all')
                .then(res =>{
                    this.groups = res.data;
                    console.log(res.data)
                })
                .catch(err =>{
                    console.log(err.message)
                })
        },
        async createGroup(){
            await axios.post('http://localhost:5000/api/group/add', {groupname:this.groupname, tagname:this.tagname, started:this.started, group_number:this.group_number, group_along:this.group_along, teacher:this.teacher})
                .then(res =>{
                    // console.log(res.data)
                    this.getGroups()
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
        <div class="groups">
            <h1>Yangi guruh qo'shish</h1>
            <select name="group" v-model="groupname" id="group">
                <option value="">Kurs nomi </option>
                <option v-for="cours in courses" :value="cours._id">{{ cours.kurs_name }}</option>
            </select>
            <input type="text" v-model="tagname" placeholder="Guruh nomini kiriting...">
            <input type="date" v-model="started">
            <input type="number" v-model="group_number" placeholder="Kurs raqami...">
            <input type="number" v-model="group_along" placeholder="Davomiyligi...">
            <select name="teach" id="teach" v-model="teacher">
                <option value="">Teacher</option>
                <option v-for="teach in teachers" :value="teach.id">{{ teach.fullname }} {{ teach.surname }}</option>
            </select>
            <button @click="createGroup">Qo'shish</button>
                     

        </div>
        <div class="groups">
            <h2>Guruhlar</h2>

            <table>
                <thead>
                    <tr>
                        <th>№</th>
                        <th>Guruh nomi</th>
                        <th>Guruh boshlanish sanasi</th>
                        <th>Guruhning davomiyligi</th>
                        <th>Guruhdagi harakatlar</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="gr in groups">
                        <td>{{ gr.id }}</td>
                        <td>{{ gr.tagname }}</td>
                        <td>{{ gr.started }}</td>
                        <td>{{ gr.group_along }}</td>
                        <td>
                            <a href="">...</a>
                        </td>
                    </tr>
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

.groups {
    width: 100%;
    min-height: 100px;
    background-color: white;
    border-radius: .6rem;
    padding: 10px;
    margin-bottom: 10px;
}

.groups input,
button,
select {
    height: 40px;
    padding: 5px;
    margin: 5px;
}
.groups table{
    border-collapse: collapse;
    width: 100%;
}
.groups tr,th,td{
    border: 1px solid black;
    padding: 3px;
}
</style>