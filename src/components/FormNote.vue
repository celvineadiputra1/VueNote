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
        name: 'FormNote',
        props: {},
    data : function(){
        return {
            id : 0,
            title : '',
            description : '',
            mode : 'save'
        }
    },
        methods: {
            submitSave() {
                let data= {
                    id : this.id,
                    title : this.title,
                    description : this.description
                }
                this.$root.$emit('emitSaveNote', data);
            },
            submitUpdate(){
                let data= {
                    id : this.id,
                    title : this.title,
                    description : this.description
                }
                this.$root.$emit('emitUpdateNote', data);
            },
            submitRemove() {
                let data = {id : this.id}
                this.$root.$emit('emitRemove', data);
                this.resetInput();
            },
            resetInput() {
                this.id = 0;
                this.title = '';
                this.description = '';
            }
        },
        mounted() {
            this.$root.$on('emitForm', data => {
                this.id = data.id;
                this.title = data.title;
                this.description = data.description;
                this.mode = data.mode;
            });
        }
    }
</script>
<style scoped>
    * {
        font-family: 'SecularOne';
    }

    .form-control {
        border: 0px !important;
    }

    .form-control:focus {
        outline: none !important;
        border: none !important;
        box-shadow: none !important;
    }
</style>