<template>
    <li class="list-group-item border-0">
        <div class="row align-items-center">
            <input class="col-1" type="checkbox" v-model="todo.completed">
            <p class="col-10 text-left text-truncate m-0">{{ todo.content}}</p>
            <button class="col-1 btn btn-primary  p-0 " @click="deleteTodo">X</button>
        </div>
    </li>
</template>
<script>
export default {
    props: {
        todo: {
            type: Object,
            required: true,
        }
    },
    methods: {
        deleteTodo: function () {
            this.$emit('del', this.todo.id)
        }
    }
}
</script>