<template>
    <p
        :id="todoProps.id"
        :class="['todo-item', todoProps.completed ? 'is-completed' : '']"
    >
        <input
            type="checkbox"
            :checked="todoProps.completed"
            @change="markItemCompleted"
        />
        {{ todoProps.title }}
        <button class="del-btn" @click="deleteItem">Delete</button>
    </p>
</template>

<script>
// import { ref } from 'vue'
export default {
    name: 'TodoItem',
    props: ['todoProps'],
    setup(props, context) {
        const markItemCompleted = () => {
            context.emit('item-completed', props.todoProps.id)
        }

        const deleteItem = () => {
            context.emit('delete-item', props.todoProps.id)
        }

        return {
            markItemCompleted,
            deleteItem
        }
    }
}
</script>

<style>
.del-btn {
    background: #f00;
    color: white;
    border: none;
    cursor: pointer;
    float: right;
}

.todo-item {
    background: #f4f4f4;
    padding: 10px;
    margin: 0;
    border-bottom: 1px #ccc solid;
}

.is-completed {
    text-decoration: line-through;
}
</style>
