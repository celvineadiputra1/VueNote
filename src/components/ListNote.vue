<template>
    <div>
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
    export default {
        name: "ListNote",
        data: function () {
            return {
                notes: [{
                    id: 1,
                    title: 'Artikel 1',
                    description: 'Des 1'
                }, {
                    id: 2,
                    title: 'Artikel 2',
                    description: 'Des 2'
                }]
            }
        },
        componets: {

        },
        props: {
            propsEditNote: {
                type: Function
            }
        },
        methods: {
            editNote(id) {
                // console.log('app ' + id);
                let dataForm = this.notes.find(notes => notes.id === id);
                this.$root.$emit('emitForm', dataForm);
                // console.log(this.dataForm);
            },
            createNewId() {
                let newId = 0;
                if (this.notes.length === 0) {
                    newId = 1;
                } else {
                    newId = this.notes[this.notes.length - 1].id + 1;
                }
                return newId;
            }
        },
        mounted() {
            this.$root.$on('emitRemove', data => {
                let noteIndex = this.notes.findIndex(notes => notes.id === data.id);
                this.notes.splice(noteIndex, 1);
            });
            this.$root.$on('emitUpdateNote', data => {
                let noteIndex = this.notes.findIndex(notes => notes.id === data.id);
                this.notes[noteIndex].title = data.title;
                this.notes[noteIndex].description = data.description;
            });
            this.$root.$on('emitSaveNote', data => {
                let newId = this.createNewId();
                let note = {
                    'id': newId,
                    'title': data.title,
                    'description': data.description
                };
                this.notes.push(note);
                this.editNote(newId);
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
</style>