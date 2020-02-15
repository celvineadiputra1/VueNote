<template>
    <div class="container-fluid p-0">
        <form>
            <div class="row bg-gray p-3">
                <div class="col-sm-12 d-flex justify-content-end">
                    <button v-if="mode == 'save'" class="btn btn-success mr-2" type="button"
                        @click="submitSave">Save</button>
                    <button v-if="mode == 'update'" class="btn btn-success mr-2" type="button"
                        @click="submitUpdate">Update</button>
                    <button class="btn btn-danger mr-2" @click="submitRemove" type="button">Delete</button>
                </div>
            </div>
            <div class="row">
                <div class="col-sm-12 pt-3">
                    <b-alert :show="dismissCountDown" fade dismissible variant="success" @dismissed="dismissCountDown=0"
                        @dismiss-count-down="countDownChanged">
                        <h2>
                            {{alert_message}}
                        </h2>
                        Close in {{ dismissCountDown }} seconds...
                    </b-alert>
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
    import axios from 'axios';
    import {
        BAlert
    } from 'bootstrap-vue';
    export default {
        name: 'FormNote',
        props: {},
        data: function () {
            return {
                id: 0,
                title: '',
                description: '',
                mode: 'save',
                alert_message: '',
                dismissSecs: 5,
                dismissCountDown: 0,
                base_url_input: 'http://localhost/ProjectVueWegodev2/note/create',
                base_url_update: 'http://localhost/ProjectVueWegodev2/note/update',
                base_url_delete: 'http://localhost/ProjectVueWegodev2/note/delete'
            }
        },
        components: {
            'b-alert': BAlert
        },
        methods: {
            countDownChanged(dismissCountDown) {
                this.dismissCountDown = dismissCountDown
            },
            submitSave() {
                let param = new URLSearchParams();
                param.append('title', this.title);
                param.append('description', this.description);
                axios.post(this.base_url_input, param).then(response => {

                    let data = {
                        id: response.data.id,
                        title: this.title,
                        description: this.description
                    }

                    this.$root.$emit('emitSaveNote', data);

                    this.alert_message = response.data.pesan;

                    this.dismissCountDown = this.dismissSecs
                });
            },
            submitUpdate() {
                let param = new URLSearchParams();
                param.append('id', this.id);
                param.append('title', this.title);
                param.append('description', this.description);

                axios.post(this.base_url_update, param).then(response => {
                    let data = {
                        id: this.id,
                        title: this.title,
                        description: this.description
                    }
                    this.$root.$emit('emitUpdateNote', data);

                    this.alert_message = response.data.pesan;
                    this.dismissCountDown = this.dismissSecs
                });
            },
            submitRemove() {
                let param = new URLSearchParams();
                param.append('id', this.id);

                axios.post(this.base_url_delete, param).then(response => {
                    let data = {
                        id: this.id
                    }
                    this.$root.$emit('emitRemove', data);

                    this.alert_message = response.data.pesan;
                    this.dismissCountDown = this.dismissSecs
                    this.resetInput();
                });
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
        font-family: 'RR';
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