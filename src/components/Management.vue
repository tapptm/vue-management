<template>
  <div class="manager">
    <h1>{{ msg }}</h1>
    <form name="todo-form" method="post" action="" v-on:submit.prevent= "addTask">
    <input type="text" v-model= "addFirstName" placeholder="ชื่อ" />
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


   <h3>List Employee</h3>
     <div class="todo-lists" v-if="lists.length">
          <ul>
            <li v-for="list in filterLists" :key="list.id">
                <input type="checkbox" v-on:change="completeTask(list)" v-bind:checked="list.isComplete"/>
                  <span class="fname"
                        contenteditable="true"
                        v-on:keydown.enter="updateTask($event, list)"
                        v-on:blur="updateTask($event, list)"
                        v-bind:class="{completed: list.isComplete}">
                        ชื่อ : {{list.fname}}</span>

                  <span class="lname"
                        contenteditable="true"
                        v-on:keydown.enter="updateTask($event, list)"
                        v-on:blur="updateTask($event, list)"
                        v-bind:class="{completed: list.isComplete}">
                        สกุล : {{list.lname}}
                  </span> 

                  <span class="age"
                        contenteditable="true"
                        v-on:keydown.enter="updateTask($event, list)"
                        v-on:blur="updateTask($event, list)"
                        v-bind:class="{completed: list.isComplete}">
                        อายุ : {{list.age}}
                  </span> 

                  <span class="selectGender" 
                         v-bind:class="{completed: list.isComplete}">
                         เพศ : {{list.gender}}
                  </span> 

                  <span class="selectPosition" 
                        v-bind:class="{completed: list.isComplete}">
                        ตำแหน่ง : {{list.position}}
                   </span> 
                   <span class="remove" v-on:click="removeTask(list)">x</span>
            </li>
          </ul>
        </div>
    
  </form>
  </div>
</template>

<script>

import _ from 'lodash'

export default {
  name: 'manage',
  props: {
    msg: String
  },
  data : function () {
   return {
     message: 'New Task',
     selected : '',
     addFirstName : ''  , 
     addLastName : '',
     addAge : '',
     selectGender : '',
     selectPosition : '',
     lists: [], // this will hold all the created todo task items
     hasError: false  // <-- to handle errors
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
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}

a {
  color: #42b983;
}

input[type=text].error{border: 1px solid red;}


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
</style>
