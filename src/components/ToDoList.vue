<template>
    <table id="TableList">
        <template v-if="!edit" >
            <tr  v-for="(todo, index) in todos" :key="index"  :class="[todo.isActive ? '' : 'DoneDeal', 'Deal']">
                <th>
                    <input @change="doneToDo(index)" :checked="!todo.isActive" :id="'check' + index" type="checkbox">
                    <label :for="'check' + index">{{ todo.name }}</label>
                </th>
            </tr>
        </template>
        <template v-else>
             <tr v-for="(todo, index) in todos" :key="index"  :class="[todo.isActive ? '' : 'DoneDeal', 'Deal']">
                <th>
                    <input  type="text" v-model="todo.name">
                </th>
                <th @click="deleteToDo(index)" >
                    <i class="fas fa-times"></i>
                </th>
            </tr>
        </template>    
    </table>
</template>

<script>
export default {
    name: 'ToDolist',
    props: ['todos', 'edit'],
    methods: {
        deleteToDo(index){
            this.$emit('delete-todo', index);
        },
        doneToDo(index){
            this.$emit('done-todo', index);
        },
        addToDo(newDeal){
            this.$emit('add-todo', newDeal);
        },
        redactToDo(index, ChangeDeal){
            this.$emit('redact-todo', index, ChangeDeal);
        }
    }
}
</script>

<style scoped>
    .Deal{
        font-size: 40px;
        color: rgb(0, 0, 0);
        }
    .DoneDeal{
          text-decoration: line-through;
          color: rgb(52, 52, 52);
        } 
    #TableList{
        width: 100%;
        background-color: rgba(255, 255, 255, 0.401);
    }
    #TableList tr {
        display: flex;
        justify-content: flex-start;
    }
    #TableList tr th:nth-child(2){
        width: 70px;
        align-self: center;
    }
    #TableList tr th:nth-child(1){
        display: flex;
        justify-content: flex-start;
        align-items: center;
        width: calc(100vw - 70px);
        text-align: left;
    }
    input[type=text] {
        width: 90%;
        height: 30px;
        font-size: 20px;
        padding: 6px 0 4px 10px;
        margin: 15px 0 15px 0;
        border: 1px solid #000000;
        background: #ff000000;
        border-radius: 2px;
    }

    input[type=checkbox] {
        margin: 0 15px 0 15px;
    }
    input[type="checkbox"] {
        display: none;
    }
    label {
        color: #000;
        cursor: default;
        font-weight: normal;
        line-height: 30px;
        padding: 10px 0;
        vertical-align: middle;
    }
    label:before {
        content: " ";
        color: #000;
        display: inline-block;
        font: 20px/30px FontAwesome;
        margin-right: 15px;
        position: relative;
        text-align: center;
        text-indent: 0px;
        width: 25px;
        height: 25px;
        border: 2px solid rgb(0, 0, 0);
        /* border-radius: 100%; */
        background: rgba(255, 255, 255, 0);
        border-image: initial;
        vertical-align: middle;
    }
    input:checked + label:before {
        content: "\f00c";
    }
</style>