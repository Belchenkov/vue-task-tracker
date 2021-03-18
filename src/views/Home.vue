<template>
    <AddTask v-if="showAddTask" @add-task="addTask" />
    <Tasks
        @delete-task="deleteTask"
        :tasks="tasks"
        @toggle-reminder="toggleReminder"
    />
</template>

<script>
import Tasks from '../components/Tasks';
import AddTask from '../components/AddTask';

export default {
    props: {
        showAddTask: Boolean
    },
    data() {
        return {
            tasks: []
        }
    },
    components: {
        Tasks,
        AddTask
    },
    async created() {
        this.tasks = await this.fetchTasks();
    },
    methods: {
        async addTask(task) {
            const res = await fetch('api/tasks', {
                method: 'POST',
                headers: {
                'Content-Type': 'application/json'
                },
                body: JSON.stringify(task)
            });

            const data = await res.json();

            this.tasks = [
                ...this.tasks,
                data
            ];
        },
        async deleteTask(id) {
            if (confirm('Are you sure?')) {
                const res = await fetch(`api/tasks/${id}`, {
                method: 'DELETE'
                });

                res.status === 200 ? (this.tasks = this.tasks.filter(task => task.id !== id)) : alert('Error Deleting Task');
            }
        },
        async toggleReminder(id) {
            const taskToToggle = await this.fetchTask(id);
            const updTask = {...taskToToggle, reminder: !taskToToggle.reminder};

            const res = await fetch('api/tasks', {
                method: 'PUT',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(updTask)
            });

            const data = await res.json();

            this.tasks = this.tasks.map(task => task.id === id ? {...task, reminder: data.reminder} : task);
        },
        async fetchTasks() {
            const res = await fetch('api/tasks');
            return  await res.json();
        },
        async fetchTask(id) {
            const res = await fetch(`api/tasks/${id}`);
            return  await res.json();
        }
    }
}
</script>

<style>

</style>