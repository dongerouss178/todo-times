<template>

<v-list two-line subheader>
  <v-container> 
      <v-flex>
      <v-subheader class="headline">YOUR TASK FOR TODAY</v-subheader>
      <v-spacer> </v-spacer>
        <p class ="text-right"><b>{{todos.length}}</b> Tasks </p>

            <v-text-field clearable v-model="newTodo" label="Please put your task here" @keyup.enter="addTodo">
            </v-text-field>
        
   
    <v-subheader class="subheading" v-if="todos.length == 0"> You have 0 Tasks, add some </v-subheader>
    <v-subheader class="subheading" v-else> Your task </v-subheader>
    <!-- <v-list> -->
        <!-- <v-list-item v-for="(todo,index) in todos" :key="todo.id"> -->
        <div v-for="(todo, index) in todos" :key="todo.id">
            <v-flex xs12>
            <v-list-item avatar>
               
                <v-list-item-action>
                    <v-checkbox v-model="todo.completed"></v-checkbox> 
                </v-list-item-action>
                <v-list-title-content v-if="!todo.editing" @dblclick="editTodo(todo)"  >
                    <v-list-title-title  :class="{completed: todo.completed}">{{todo.title}}</v-list-title-title>
                </v-list-title-content>   
                
                <v-text-field v-else v-model="todo.title" @blur="doneEdit(todo)" @keyup.enter="doneEdit(todo)" autofocus="true" > </v-text-field> 
               
                <v-spacer></v-spacer>
                
                <v-list-item-action>
                <v-btn icon @click="removeTodo(index)" >
                    <v-icon small size="small" color="grey lighten -1" class="remove">x</v-icon>
                </v-btn>
                </v-list-item-action>
                
                
                <!-- create a function when user double click to the name it will give them chance to edit -->
                 
           
             
          
            
                <!-- <v-tooltip v-model="show" top>
                    <template v-slot:activator="{off}"> -->
                        <!-- <v-btn icon v-on="off" @click="removeTodo(index)">
                            <v-icon color="grey lighten -1" size="small">x</v-icon>
                        </v-btn> -->
                    <!-- </template> 
                </v-tooltip> -->
        <!-- </v-list-item-tile> -->
                
           </v-list-item> 
            </v-flex>
        </div>  
        
    <!-- </v-list> -->

        <v-divider> </v-divider>
      </v-flex>      
 </v-container>
      
</v-list>

</template>

<script>
  export default {
    name: 'todo-list',

    data () {
        return{
            newTodo:'',
            idForTodo:2,
            beforeEditCache: '',
            todos: [ 
                
            ]
        }
    },

    directives:
    {
        focus: {
            inserted: function (el) {
                el.focus()
            }
        }
    },
        // create method to add list
    methods: {
        // method to add user's input to the list of todo
        addTodo() 
        {
            // 
            if (this.newTodo.trim().length == '' ) {
                
                return 
            }

                this.todos.push({
                    id: this.idForTodo,
                    title: this.newTodo,
                    completed: false,
                    editing : false,

                })

                this.newTodo = ''
                this.idForTodo++
        },

        removeTodo(index)
        {
                this.todos.splice(index,1)
        },

        editTodo(todo) 
        {
                this.beforeEditCache = todo.title
                todo.editing = true
        },
            
        doneEdit(todo) 
        {
                     if (todo.title.trim()== "" ) {
    
                todo.title = this.beforeEditCache
            
           }
                todo.editing = false
       
        },

            cancelEdit (todo){
                todo.title= this.beforeEditCache
                todo.editing = false
            }
        }
    }
     
</script>

<style>



    
    .completed{
        text-decoration: line-through;
        color:grey;
    }

    .remove{
        cursor: pointer;
        margin-left: 14px;
       
    }
</style>
