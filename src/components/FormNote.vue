<template>
    <div class="container-fluid mt-3">
        <form @submit="submitNote">
            <div class="row">
                <div class="col-sm-12 d-flex justify-content-end">
                    <button class="btn btn-success mr-2" type="submit">Save</button>
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
        props: {
            propsSaveNote: {
                type: Function
            },
            propsUpdateNote: {
                type: Function
            }
        },
        data: function () {
            return {
                id: 0,
                title: '',
                description: ''
            }
        },
        methods: {
            submitNote(e) {
                e.preventDefault();
                let data = {
                        title : this.title,
                        description : this.description
                    }
                console.log(this.title);
                if (this.id == 0) {
                    this.$root.$emit('emitSaveNote', data);
                } else {
                    data.id = this.id;
                    this.$root.$emit('emitUpdateNote', data);
                }
                this.resetInput();
            },
            submitRemove(e) {
                e.preventDefault();
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