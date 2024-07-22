<script setup>
import { ref, onMounted } from "vue";

const name = ref("John Doe");
const status = ref("inactive");
const tasks = ref([""]);
const newTask = ref("");

const toggleStatus = () => {
    if (status.value === "active") {
        status.value = "pending";
    } else if (status.value === "pending") {
        status.value = "inactive";
    } else {
        status.value = "active";
    }
};

const addTask = () => {
    if (newTask.value.trim() != "") {
        tasks.value.push(newTask.value);
        newTask.value = "";
    }
};

const deleteTask = (index) => {
    tasks.value.splice(index, 1);
};

onMounted(async () => {
    try {
        const response = await fetch(
            "https://jsonplaceholder.typicode.com/todos",
        );
        const data = await response.json();
        tasks.value = data.map((task) => task.title);
    } catch (error) {
        console.log("Error fetching tasks:", error);
    }
});
</script>

<template>
    <h1>{{ name }}</h1>
    <p v-if="status === 'active'">User is active</p>
    <p v-if="status === 'pending'">User is pending</p>
    <p v-if="status === 'inactive'">User is inactive</p>

    <form @submit.prevent="addTask">
        <label for="newTask">Add Task</label>
        <input type="text" id="newTask" name="newTask" v-model="newTask" />
        <button type="submit">Submit</button>
    </form>

    <h3>Tasks:</h3>
    <ul v-for="(task, index) in tasks" :key="task">
        <li>
            <span>
                {{ task }}
            </span>
            <button @click="deleteTask(index)">X</button>
        </li>
    </ul>
    <br />
    <button @click="toggleStatus">Change Status</button>
</template>
