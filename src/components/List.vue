<template>
    <div class="card-body">
        <div class="row">
            <ul class="group-list">
            <li class="list-group-item" v-for="(todo, index) in todos" :key="index">
                <div class="d-flex justify-content-between">
                    <span v-if="todo.isDone"><del>{{todo.activity}}</del></span>
                    <span v-else>{{ todo.activity }}</span>
                    <div>
                        <button @click="doneTodo(index)" class="btn btn-info">Done</button>
                    </div>
                    <div>
                        <button @click="deleteTodo(index)" class="btn btn-danger">X</button>
                    </div>
                </div>
            </li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        todos: {
            type: Array,
            default: []
        }
    },
    methods: {
        deleteTodo(index) {
            this.$emit('deleteTodo', index);
        },
        doneTodo(index) {
            this.$emit('doneTodo', index)
        }
    },
}
</script>