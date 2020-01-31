<template>
    <div>
        <button type="button" class="btn btn-primary py-0 mt-2">
        Left<span class="badge badge-light ml-2">{{ unFinishedTodoLenth }}</span>
        <span class="sr-only">items left</span>
        </button>
        <button type="button" class="btn btn-primary ml-2 py-0 mt-2"
            v-for="state in states"
            :key="state"
            :class="filter === state ? 'active' : '' "
            @click="toggleFilter(state)"
        >
            {{state}}
        </button>
        <button @click="clearAllCompleted" class="btn btn-primary py-0 ml-2 mt-2">
            Clear completed
        </button>
    </div>
</template>
<script>
export default {
    props: {
        todos: {
            type: Array,
            required: true
        },
        filter: {
            type: String,
            required: true
        }
    },
    data() {
        return {
            states: [
                "all",
                "active",
                "completed"
            ]
        }
    },
    computed: {
        unFinishedTodoLenth() {
            return this.todos.filter(todo => !todo.completed).length
        }
    },
    methods: {
        clearAllCompleted: function () {
            this.$emit('clearAllCompleted')
        },
        toggleFilter: function (state) {
            this.$emit('toggle', state)
        }
    }
}
</script>