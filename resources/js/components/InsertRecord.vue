<template>
    <div class="modal" tabindex="-1" role="dialog" id="exampleModal" aria-labelledby="exampleModalLabel" aria-hidden="true" q   >
        <div class="modal-dialog" role="document">
            <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title">Insert Record</h5>
                <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                <span aria-hidden="true">&times;</span>
                </button>
            </div>
            <div class="modal-body">
                <p class="alert alert-success" v-if="success.length > 0">{{success}}</p>
                <label>Enter todo</label>
                <input type="text" class="form-control form-control-lg" name="title" id="title"
                        v-model="record" placeholder="Enter Title for your Todo"/>
            </div>
            <div class="modal-footer">
                <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
                <button type="button" class="btn btn-primary" v-on:click="addRecord">Save changes</button>
            </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return {
            record: "", 
            success: ""
        }
    },
    methods:{
        addRecord(){
            axios.post('http://localhost:8000/tasks', {
                'title': this.record,
                'user_id' : 1
            })  
            .then(data => {
                this.$emit('recordadded', data);
                this.success = "New record added successfully";
                })
            .catch(error => console.log(error))
        }
    }
}
</script>

<style scoped>

</style>
