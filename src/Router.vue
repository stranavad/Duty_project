<script setup>
import { ref, computed } from 'vue';
import Dashboard from '@/pages/DashBoard.vue';
import StudentsTable from "@/pages/StudentsTable.vue";

const routes = {
    "/": {
        component: Dashboard,
        title: "Dashboard"
    },
    "/students-table": {
        component: StudentsTable,
        title: "Students table"
    }
}
const currentPath = ref(window.location.hash);

window.addEventListener('hashchange', () => {
    console.log('hash change');
    currentPath.value = window.location.hash;
})


const currentView = computed(() => {
    return routes[currentPath.value.slice(1) || '/'].component || <a>not found</a>
})

</script>

<template>
    <div class="menu">
        <div>
            <a v-for="(route, index) in Object.keys(routes)" :key="index" :href="`#${route}`">{{routes[route].title}}</a>
        </div>
    </div>
    <div class="content">
        <component :is="currentView"/>
    </div>
</template>

<style scoped lang="scss">

$menuHeight: 50px;

.menu {
    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    height: $menuHeight;
    background-color: #cccccc;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: flex-end;
    padding: 0 30px;

    a {
        margin: 0 15px;
        text-decoration: none;
        color: #000000;
        font-weight: 600;
        transition: color 100ms;

        &:hover {
            color: #777777;
       }
    }
}

.content {
  margin-top: $menuHeight;
}

</style>