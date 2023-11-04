<template>
    <div>
        <Table 
            :projects="projects" 
        />
    </div>
</template>

<script>
// @ is an alias to /src
import Table from '@/components/Table.vue'

export default {
    data() {
        return {
            projects: [],
        }
    },
    name: 'MainPage',
    components: {
        Table
    },
    methods: {
        getTable() {
            fetch('http://localhost:8000/main')
                .then(response => response.json())
                .then(data => this.projects = data);
        }
    },
    mounted() {
        this.getTable();
    }
}
</script>

<style>
</style>