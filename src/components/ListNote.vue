<template>
    <div>
        <ul class="list-group">
            <li v-for="(row, index) in notes" :key="index" class="list-group-item mb-2" @click="idNote(row.id)">
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
    name : "ListNote",
    data : function(){
        notes : [
            {
                id : 1,
                title : 'Artikel 1',
                description : 'Des 1'
            },{
                id : 2,
                title : 'Artikel 2',
                description : 'Des 2'
            }
        ];
    },
    componets:{

    },
    props : {
        propsNotes : {
            type : Array
        },
        propsEditNote : {
            type : Function
        }
    },
    methods:{
        idNote(id){
            this.propsEditNote(id);
            console.log(id);
        }
    }
}
</script>

<style scoped>
.fontDes{
    font-family: 'SecularOne' !important;
    font-size: 12px;
}
.border-top-1{
    border-top: 1px solid black;
}
.list-group-item:hover{
    background-color: rgba(0, 0, 0, 0.123);
    cursor: pointer;
}
</style>