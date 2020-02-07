<template>
  <div id="app">
    <div class="container-fluid">
      <div class="row">
        <div class="col-sm-12 col-md-2">
          <div class="container border-bottom-1 pb-3">
            <div class="row">
              <div class="col-sm-12">
                <h1>
                  Logo
                </h1>
              </div>
            </div>
          </div>
          <ListNote />
        </div>
        <div class="col-sm-12 col-md-10">
          <FormNote />
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
    components: {
      FormNote,
      ListNote
    },
    methods: {

    }
  }
</script>

<style scoped>
  * {
    padding: 0;
    margin: 0;
  }
  .border-bottom-1{
    border: 0px;
    border-bottom: 1px solid black;
  }
</style>