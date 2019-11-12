<template>
    <div>{{aaa}}
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
export default {
  name: 'lists',
  props:{
    aaa: Number
  },

  data : function() {
    
    
  },
  methods : {
  
  }
  
}
</script>

<style>

</style>
