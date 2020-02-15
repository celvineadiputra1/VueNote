<template>
    <div class="max-100">
        <ul class="list-group">
            <li v-for="(row, index) in notes" :key="index" class="list-group-item mb-2" @click="editNote(row.id)">
                <label class="d-block">{{row.title}}</label>
                <span class="d-block fontDes border-top-1">
                    {{row.description}}
                </span>
            </li>
        </ul>
    </div>
</template>

<script>
    import axios from 'axios';
    export default {
        name: "ListNote",
        data: function () {
            return {
                notes: [],
                base_url_get : 'http://localhost/ProjectVueWegodev2/note'
            }
        },
        componets: {

        },
        methods: {
            editNote(id) {
                let dataForm = this.notes.find(notes => notes.id === id);
                dataForm.mode = 'update';
                this.$root.$emit('emitForm', dataForm);
            },
            getData(){
                axios.get(this.base_url_get).then(response =>{
                    this.notes = response.data;
                    console.table(this.notes);
                });
            }
        },
        mounted() {
            this.getData();
            this.$root.$on('emitRemove', data => {
                let noteIndex = this.notes.findIndex(notes => notes.id === data.id);
                this.notes.splice(noteIndex, 1);
            });
            this.$root.$on('emitUpdateNote', data => {
                console.log(data.id);
                let noteIndex = this.notes.findIndex(notes => notes.id === data.id);
                this.notes[noteIndex].title = data.title;
                this.notes[noteIndex].description = data.description;
            });
            this.$root.$on('emitSaveNote', data => {
                let note = {
                    'id': data.id,
                    'title': data.title,
                    'description': data.description
                };
                this.notes.unshift(note);
                this.editNote(data.id);
            });
        }
    }
</script>

<style scoped>
    .fontDes {
        font-family: 'SecularOne' !important;
        font-size: 12px;
    }

    .border-top-1 {
        border-top: 1px solid black;
    }

    .list-group-item:hover {
        background-color: rgba(0, 0, 0, 0.123);
        cursor: pointer;
    }
    .max-100{
        max-height: calc(100vh - 9rem);
        overflow-y: scroll;
    }
    ui > li {
        cursor: pointer;
    }
</style>