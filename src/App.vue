<template>
  <div id="app">
    <div class="container-fluid">
      <div class="row">
        <div class="col-sm-12 col-md-2 bg-gray min-vh-100 border-right-1">
          <div class="container border-bottom-1 pb-3">
            <div class="row">
              <div class="col-sm-12">
                <h1>
                  Logo
                </h1>
              </div>
            </div>
          </div>
          <button class="btn btn-primary w-100 mb-2 mt-2 text-left" @click="newNote">
            + New Note
          </button>
          <ListNote :propsNotes="notes"/>
        </div>
        <div class="col-sm-12 col-md-10">
          <FormNote/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import FormNote from './components/FormNote.vue'
  import ListNote from './components/ListNote.vue'
  export default {
    name: 'app',
    data : function(){
      return{
        notes : []
      }
    },
    components: {
      FormNote,
      ListNote
    },
    methods: {
      newNote(){
        let dataForm = {'id':0,'title': '','description' : '', mode:'save'}
        this.$root.$emit('emitForm', dataForm);
      }
  }
  }
</script>

<style scoped>
  .border-bottom-1{
    border: 0px;
    border-bottom: 1px solid black;
  }
</style>