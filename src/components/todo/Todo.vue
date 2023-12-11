<template>
    <main>
        <button class="btn btn-dark btn-lg p-3 my-4" id="añadir-todo" @click=handleModal>Añadir Tarea</button>
        <div id="todos-container">
            <h1 class="w-100 text-start text-decoration-underline">Tareas Pendientes:</h1>
            <div id="todos" class="mt-5">
                <template v-if="todos">
                    <template v-for="todo in todos" :key=todo.id>
                        <IndividualTodo :data=todo :delete=this.delete :changeEdit=changeEdit />
                    </template>
                </template>
            </div>
        </div>
    </main>
</template>

<script>
import IndividualTodo from './IndividualTodo.vue';
export default {
    name: "ToDo",
    props: ["changeModal", "data", "todos", "delete", "changeEdit"],
    methods: {
        handleModal() {
            this.changeModal()
        }
    },
    data() {
        return {
            ejemplo: { title: 'hola', description: "asdas", fecha: "Hoy", id: 3 }
        }
    },
    components: {
        IndividualTodo
    }
}


</script>

<style>
main {
    min-height: 100vh;
    padding: 1rem 2rem;
    height: auto;
}

#añadir-todo {
    width: 50%;
}

#todos {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
    gap: 4rem;
    width: 100%;
    height: 100%;
}
</style>