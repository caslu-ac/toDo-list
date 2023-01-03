
<template>
    <div class="toDo-list">
    <h1>ToDo list</h1>
    <input type="text" @change="addToList" v-model="text" class="text-field">
    <ul>
        <li v-for="(item, index) in list" :key="index">
            <span @click="toggleCheckBox(item)" >
                <input type="checkbox" id="checkBox" :checked="item.done" class="check">

                <span :class="{'done' : item.done}"> {{ item.label }}</span> 
            </span>
            <span @click="deleteFromList('index')" class="delete"> delete</span>
        </li>
    </ul>

</div>
</template>

<script>
export default {
    data() {
        return {
            list: [],
            text: ''
        }
    },
    created() {
        this.list = JSON.parse(localStorage.getItem('list')) || [];
    },
    methods: {
        addToList() {
            this.list.unshift({label: this.text, done: false});
            localStorage.setItem('list', JSON.stringify(this.list))
            this.text = '';

        },
        deleteFromList() {
            this.list.splice('index', 1);
            this.updateLocalStorage();
          
        },
        updateLocalStorage(){
            localStorage.setItem('list', JSON.stringify(this.list))
        }, 
        toggleCheckBox(item){
            item.done = !item.done;
          this.updateLocalStorage();
        }
    },
}

</script>

<style>
    .toDo-list{
max-width: 500px;
margin: auto;
}
h1{
    text-align: center;
}
.text-field{
    width: 100%;
    height: 35px;
    margin-bottom: 15px;
}
ul{
    list-style: none;
    padding: 0;
}

li{
    display: flex;
    justify-content: space-between;
    padding: 5px;
}
ul li .delete{
    background-color:red;
    border-radius: 12px;
    padding: 0 5px 0 5px;
    color: white;
}
.done{
    text-decoration: line-through;
}



</style>