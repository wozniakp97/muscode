<template>
    <div class="toDoListContainer">
        <div class="textContainer">
            <p>Lista ToDo</p>
            <p>Wykonane: {{ toDoList.filter(el => el.done == true).length }}</p>
        </div>
        <div class="checkboxContainer">
            <label v-for="iteam in toDoList" :key="iteam.id">
                <input type="radio" :checked="iteam.done" @click="iteam.done = !iteam.done">
                {{ iteam.name }}</label>
            <label>
                <input type="text" placeholder="+ Dodaj nowy element checklisty" class="inputClass" v-model="toDoIteam"
                    @keyup.enter="el => addToDo(el.target.value)">
            </label>
        </div>
    </div>
</template>
    
<script>

import { ref } from 'vue'

export default {
    name: 'ToDoList',
    props: {
        toDoList: {
            type: Array
        }
    },
    setup(props, { emit }) {

        const toDoIteam = ref('')

        function addToDo(el) {
            emit('addToDo', el)
            toDoIteam.value = ''
        }
        return { addToDo, toDoIteam }
    }
}
</script>
    
<style lang="scss" scoped>
.inputClass {
    margin: 6px 5px;
    border: none;
    width: 300px;

    &:focus {
        outline: none;
    }

    &:placeholder-shown+.label {
        opacity: 0;
        visibility: hidden;
        transform: translateY(-40px);
    }
}

label {
    text-align: left;
    border-bottom: 1px solid #b2b2b2;
    width: 100%;
    margin: 6px 0;
}

.textContainer {
    display: flex;
    justify-content: space-between;
    margin: 0 10px;
}

.checkboxContainer {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    margin: 0 10px;
}

.toDoListContainer {
    box-shadow: 0 0 15px 0px #adadad;
    background-color: #ffffff;
    border: 1px solid #b2b2b2;
    border-radius: 8px;
    height: -webkit-fill-available;
}
</style>