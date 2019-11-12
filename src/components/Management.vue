<template>
  <div class="manager">
    <h1>{{ msg }}</h1>

    <lists/>

    <form id="form" name="todo-form" method="post" action="" v-on:submit.prevent= "addTask">
    <input type="text" v-model= "addFirstName " placeholder="ชื่อ" />
    <input type="text" v-model= "addLastName" placeholder="นามสกุล" />
    <input type="number" v-model= "addAge" placeholder="อายุ" />
    <select v-model="selectGender">
        <option disabled value="">เพศ</option>
        <option>ชาย</option>
        <option>หญิง</option>
    </select>
    <select v-model="selectPosition">
        <option disabled value="">ตำแหน่ง</option>
        <option>ขายไก่</option>
        <option>ขายหมู</option>
    </select>
    <button type="submit">Add</button>
    </form>

   <h3>List Employee</h3>
   <center>
     <table >
         <thead>
             <tr>
                 <th v-bind:key="column" v-for="column in columns">
                     {{column}}
                 </th>
             </tr>
         </thead>
          <tbody>
            <tr v-for="list in filterLists" :key="list.id">
                <td>
                    <input type="checkbox" v-on:change="completeTask(list)" v-bind:checked="list.isComplete"/>
                </td>
                  <td class="fname"
                        contenteditable="true" 
                        v-on:keydown.enter="updateTask($event, list)" 
                        v-on:blur="updateTask($event, list)"
                        v-bind:class="{completed: list.isComplete}">
                        {{list.fname}}</td>

                  <td class="lname"
                        contenteditable="true" 
                        v-on:keydown.enter="updateTask($event, list)" 
                        v-on:blur="updateTask($event, list)" 
                        v-bind:class="{completed: list.isComplete}">
                        {{list.lname}}
                  </td> 

                  <td class="age"
                        contenteditable="true" 
                        v-on:keydown.enter="updateTask($event, list)" 
                        v-on:blur="updateTask($event, list)" 
                        v-bind:class="{completed: list.isComplete}">
                        {{list.age}} 
                  </td> 

                  <td class="selectGender" 
                        contenteditable="true" 
                        v-on:keydown.enter="updateTask($event, list)" 
                        v-on:blur="updateTask($event, list)" 
                        v-bind:class="{completed: list.isComplete}">
                        {{list.gender}}
                  </td> 

                  <td class="selectPosition" 
                        contenteditable="true" 
                        v-on:keydown.enter="updateTask($event, list)" 
                        v-on:blur="updateTask($event, list)" 
                        v-bind:class="{completed: list.isComplete}">
                        {{list.position}}
                  </td> 
                  <td>
                        <a href="#editform" class="remove" v-on:click="removeTask(list)">edit</a>
                  </td>
                  <td >  
                        <a href="#!" class="remove" v-on:click="removeTask(list)">x</a>
                  </td>
            </tr>
          </tbody>
        </table>
    </center>
  
  </div>
</template>

<script>

import _ from 'lodash'
import lists from '../components/ListEmployee.vue'

export default {
  name: 'manage',
  props: {
    msg: String
  },
  component:{
      lists
  },

  data : function () {
   return {
     columns: ['สถานะ', 'ชื่อ', 'นามสกุล', 'อายุ', 'เพศ', 'ตำแหน่ง','แก้ไข','ลบ'],
     selected : '',
     addFirstName : ''  , 
     addLastName : '',
     addAge : '',
     selectGender : '',
     selectPosition : '',
     lists: [], // this will hold all the created todo task items
     editInput: {
                fname: "",
                lname: "",
                age: "",
                gender: "",
                position: ""
                }
                 

   }
    
  },
  computed: {
    filterLists: function(){
      return _.orderBy(this.lists, ['isComplete', false])
    }
  },
  methods:{
    addTask: function(){  //form submit action goes here
     this.lists.push({
        id: this.lists.length+1,
        first : this.selected,
        fname: this.addFirstName,
        lname : this.addLastName,
        age : this.addAge,
        gender : this.selectGender,
        position : this.selectPosition,
        isComplete: false
      });
      this.addFirstName = ''; //clear the input after successful submission
      this.addLastName = '';
      this.addAge = '';
      this.selectGender = '';
      this.selectPosition = '';
      
    },
    editTask: function(index) {
      this.editInput = this.list[index];
      this.list.splice(index, 1);
    },
    completeTask: function(list){
            list.isComplete = !list.isComplete;
    },
    removeTask: function(list){
      var index = _.findIndex(this.lists, list);
      this.lists.splice(index, 1);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.completed{
  text-decoration: line-through;
}
.remove{
  cursor:pointer;
  display:inline-block;
  border: 1px solid #c4c4c4;
  border-radius: 50%;
  padding:0px 4px;
}
.remove:hover{
  background: #3cb0fd;
}

table {
  border-collapse: collapse;
  width: 50%;
}

table, th, td {
  border: 1px solid black;
  height: 20px;
}
</style>
