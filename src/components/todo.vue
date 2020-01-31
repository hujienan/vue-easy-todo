<template>
    <div class="container">
        <div class="col-sm-12 col-lg-6 mx-auto">
            <input class="col-8 col-lg-5 border-0 text-center mb-4 input-todo" type="text" placeholder="What to do?" @keyup.enter="addTodo">
            <ul class="list-group">
                <Item
                    v-for="todo in filteredTodos"
                    :key="todo.id"
                    :todo="todo"
                    @del="deleteTodo"
                ></Item>
            </ul>
            <Tabs
                :todos="todos"
                :filter="filter"
                @toggle="toggleFilter"
                @clearAllCompleted="clearAllCompleted"
            ></Tabs>
        </div>
    </div>
</template>
<script>
import Item from './item.vue'
import Tabs from './tabs.vue'
let id = 0
export default {
    data() {
        return {
            todos: [],
            filter: 'all'
        }
    },
    components: {
        Item,
        Tabs
    },
    computed: {
        filteredTodos () {
            if (this.filter === 'completed') {
                return this.todos.filter(todo => todo.completed)
            }
            if (this.filter == 'active') {
                return this.todos.filter(todo => !todo.completed)
            }
            return this.todos
        }
    },
    methods: {
        addTodo: function (e) {
            this.todos.unshift({
                id: id++,
                content: e.target.value.trim(),
                completed: false
            })
            e.target.value = ""
        },
        deleteTodo: function (id) {
            this.todos.splice(this.todos.findIndex(todo => todo.id == id), 1)
        },
        toggleFilter: function (state) {
            this.filter = state
        },
        clearAllCompleted: function () {
            this.todos = this.todos.filter(todo => !todo.completed)
        }
    }
}
</script>
<style>
    input.input-todo:focus {
        outline-style: none;
    }
    .input-todo {
        font-size: 1.5rem;
        font-weight: bold;
        line-height: 2;
    }
</style>