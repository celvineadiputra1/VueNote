<template>
    <div class="container-fluid mt-3">
        <form>
            <div class="row">
            <div class="col-sm-12 d-flex justify-content-end">
                <button v-if="mode == 'save'" class="btn btn-success mr-2" type="button" @click="submitSave">Save</button>
                <button v-if="mode == 'update'" class="btn btn-success mr-2" type="button" @click="submitUpdate">Update</button>
                <button class="btn btn-danger mr-2" @click="submitRemove">Delete</button>
            </div>
        </div>
        <div class="row mt-4">
            <div class="col-sm-12">
                <div class="form-group">
                    <input type="text" class="form-control" placeholder="id" v-model="id">
                    <input type="text" class="form-control" placeholder="Judul" v-model="title">
                    <textarea class="form-control" placeholder="Rencana anda" v-model="description"></textarea>
                </div>
            </div>
        </div>
        </form>
    </div>
</template>

<script>
export default {
    name : 'FormNote',
    props: {
        propsSaveNote : {
            type : Function
        },
        propsDataForm : {
            type : Object
        },
        propsUpdateNote: {
            type : Function
        },
        propsRemoveNote: {
            type : Function
        }
    },
    data : function(){
        return {
            id : 0,
            title : '',
            description : '',
            mode : 'save'
        }
    },
    methods : {
        submitSave(){
            this.propsSaveNote(this.id,this.title, this.description);
            this.resetInput();
        },
        submitUpdate(){
            this.propsUpdateNote(this.id, this.title, this.description);
        },
        submitRemove(e){
            e.preventDefault();
            this.propsRemoveNote(this.id);
            this.resetInput();
        },
        resetInput(){
            this.id = 0;
            this.title = '';
            this.description = '';
        }
    },
    watch: {
        propsDataForm: function(note){
            this.id = note.id
            this.title = note.title
            this.description = note.description
            this.mode = note.mode
        }
    }
}
</script>
<style scoped>
*{
    font-family: 'SecularOne';
}
.form-control{
    border: 0px !important;
}
.form-control:focus{
    outline: none !important;
    border: none !important;
    box-shadow: none !important;
}
</style>