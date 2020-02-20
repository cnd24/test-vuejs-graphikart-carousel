<template>
    <section class="todoapp">
        <header class="header">
            <h1>Carousel</h1>
            <input type="text" class="new-todo" placeholder="Ajouter une tâche" v-model="newTodo" @keyup.enter="addTodo">
        </header>
        <div class="main">
            <input type="checkbox" id="toggle-all" class="toggle-all" v-model="allDone">
            <label for="toggle-all"></label>
            <ul class="todo-list">
                <li class="todo" v-for="todo in filteredTodos" :key="todo" :class="{completed: todo.completed, editing: todo === editing}">
                    <div>
                        <input type="checkbox" class="toggle" v-model="todo.completed">
                        <label @dblclick="editTodo(todo)">{{ todo.name }}</label>
                        <button class="destroy" @click.prevent="deleteTodo(todo)"></button>
                    </div>
                    <input type="text" class="edit" v-model="todo.name" @keyup.enter="doneEdit" @blur="doneEdit" @keyup.esc="cancelEdit" v-focus="todo === editing">
                </li>
            </ul>
            <button class="clear-completed" v-show="completed" @click.prevent="clearCompleted">Clear completed</button>
        </div>
        <footer class="footer" v-show="hasTodos">
            <span class="todo-count">{{ remaining }} tâche(s) à faire</span>
            <ul class="filters">
                <li><a href="#" :class="{selected: filter === 'all'}" @click.prevent="filter = 'all'">Toutes</a></li>
                <li><a href="#" :class="{selected: filter === 'todo'}" @click.prevent="filter = 'todo'">A faire</a></li>
                <li><a href="#" :class="{selected: filter === 'done'}" @click.prevent="filter = 'done'">Faites</a></li>
            </ul>


        </footer>
    </section>
</template>

<script>
    import Vue from 'vue'

    export default{
        data(){
            return {
                todos: [{
                    name: 'Première tâche',
                    completed: false,
                }],
                newTodo: '',
                filter: 'all',
                editing: null,
                oldTodo: ''
            }
        },
        methods:{
            addTodo() {
                this.todos.push({
                    name: this.newTodo,
                    completed: false
                })
                this.newTodo = ''
            },
            deleteTodo(todo) {
                this.todos.splice(todo, 1)
            },
            clearCompleted() {
                this.todos = this.todos.filter(todo => !todo.completed)
            },
            editTodo(todo){
                this.editing = todo
                this.oldTodo = todo.name
            },
            doneEdit() {
                this.editing = null
            },
            cancelEdit() {
                this.editing.name = this.oldTodo
                this.doneEdit()
            },
        },
        computed: {
            completed () {
                return this.todos.filter(todo => todo.completed).length
            },
            allDone: { /* elle dépend d'autres variables donc computed  */
                get () {/* elle est dans un v-model donc elle aura des setters et getters */
                    return this.remaining === 0
                },
                set (value) {
                  if (value === true) {
                      this.todos.forEach(todo => {todo.completed = true})
                  } else {
                      this.todos.forEach(todo => {todo.completed = false})
                  }
                }
            },
            remaining() {
                return this.todos.filter(todo => !todo.completed).length
            },
            filteredTodos () {
                if(this.filter === 'todo') {
                    return this.todos.filter(todo => !todo.completed)
                } else if (this.filter === 'done') {
                    return this.todos.filter(todo => todo.completed)
                }
                return this.todos
            },
            hasTodos () {
                return this.todos.length > 0
            }
        },
        directives: {
            focus: function (el, value) {
                if(value) {
                    // eslint-disable-next-line no-unused-vars
                    Vue.nextTick(_ => {el.focus()})
                }
            }
        }
    }
</script>

<style src="./todos.css"></style>