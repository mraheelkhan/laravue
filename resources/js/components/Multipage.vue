<template>

     <div class="row">
        <div class="col-md-8">
            <insert-record @recordadded="refreshRecord"></insert-record>
            <button type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModal">
                Launch demo modal
                </button>
                 <ul class="list-group" >
                    <li v-for="todo in tasks.data" v-bind:key="" class="list-group-item" >{{todo.id}} - {{todo.title}}</li>
                </ul>
                <pagination :data="tasks" @pagination-change-page="getResults"></pagination>
        </div>
    </div>
</template>
<script>
import CardView from './CardView.vue';
import Login from './Login.vue';
import InsertRecord from './InsertRecord.vue';
export default {
    name: 'Multipage',
    components: {CardView, Login, InsertRecord},
    data(){
        return{
            tasks:{}
        }
    },
    methods:{
        getResults(page = 1) {  
			axios.get('http://localhost:8000/tasks?page=' + page)
				 .then( (response) => this.tasks = response.data)
                .catch((error) => console.log(error))
        },
        refreshRecord(record){
            this.tasks = record.data;
        }
    },
    computed:{

    },
    mounted(){
        console.log('multi mounted');
        axios.get('http://localhost:8000/tasks')
        .then( (response) => this.tasks = response.data)
        .catch((errors) => console.log(errors))
    },
    created(){
        console.log('the component has been created by vuejs')
        
    },
}
</script>

