<template>
  <div class='home'>
     <h1 class='title'>Vuengo</h1>
     <hr>
     <div class="">
       <div class="column is-3 is-offset-3">'
        <form @submit.prevent="addTask">
            <h2 class="subtitle">Add Task</h2>
            <div class="field">
                <label class="label">Description</label>
            <div class="control">
                <input class="input" type="text" v-model="description">
            </div>
            </div>
            <div class="field">
                <label class="label">Status</label>
            <div class="control">
                <div class="select">
                    <select v-model="status">
                     <option value="todo">To Do</option>
                     <option value="done">Done</option>
                    </select>


                </div>

            </div>
            </div>
            <div class="field">
            <div class="control">
                <button class="button is-link">Submit</button>
            </div>
            </div>
        </form>
       </div>

     </div>
  <div class="columns">
  <div class="column is-6">
    <h2 class="subtitle">To do</h2>
  <div class="todo">
    <div class="card" v-for="task in tasks" :key="task" >
    <div class="card-content">
        {{task.description}}
    </div>
    <footer class='card-footer'>
     <a class="card-footer-item">Done</a>
    </footer>
    </div>
  </div>
  </div>
   <div class="column is-6">
    <h2 class="subtitle">To do</h2>
  </div>
  </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
    name:'HomePage',
    data(){
        return {
            tasks:[],
            description:'',
            status:'todo'

        }
    }, 
    mounted(){
      this.getTasks()
    },
    methods:{
        getTasks(){
            axios({
                method:'get',
                url:'http://127.0.0.1:8000/tasks/',
                auth:{
                    username:'Samanja',
                    password:'root'
                }
            }).then(response => this.tasks = response.data)
        },
        addTask(){
            if(this.description){
                axios({
                    method:'post',
                    url:'http://127.0.0.1:8000/tasks/',
                    data:{
                        description:this.description,
                        status:this.status
                    },
                    auth:{
                        username:'Samanja',
                        password:'root'
                    }
                }).then((response) => {
                    let newTask = {
                        'id':response.data.id,
                        'description':this.description,
                        'status':this.status
                    }

                    this.tasks.push(newTask)
                    this.description=''
                    this.status='todo'
                }).catch((error) =>{
                    console.log(error)
                })
            }
        }
    }

}
</script>

<style>

</style>