<script>
export default {
    data() {
        return {
            name: "John Doe",
            status: "pending",
            tasks: ["Task One", "Task Two", "Task Three"],
            link: "https://www.google.com",
        };
    },
    methods: {
        toggleStatus() {
            if (this.status === "active") {
                this.status = "pending";
            } else if (this.status === "pending") {
                this.status = "inactive";
            } else {
                this.status = "active";
            }
        },
    },
};
</script>

<template>
    <h1>{{ name }}</h1>
    <p v-if="status === 'active'">User is active</p>
    <p v-if="status === 'pending'">User is pending</p>
    <p v-if="status === 'inactive'">User is inactive</p>
    <!-- <p v-else>User is inactive</p> -->
    <!-- <p v-if="status === 'inactive'">User is inactive</p> -->
    <h3>Tasks:</h3>
    <ul v-for="task in tasks" :key="task">
        <li>{{ task }}</li>
    </ul>
    <a :href="link">Click me for Google</a>
    <br />
    <button @click="toggleStatus">Change Status</button>
</template>
