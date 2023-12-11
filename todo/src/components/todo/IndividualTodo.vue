<template>
    <div class="row" id="individual-todo">
        <div class="col-6 d-flex justify-content-center align-items-center gap-3" id="todo-buttons-container">
            <button class="boton-todo bg-primary" @click="handleEdit"><i class="fa-solid fa-pen-to-square fa-2xl"
                    style="color:white"></i></button>
            <button class="boton-todo bg-danger" @click=handleDelete><i class="fa-solid fa-trash fa-2xl"
                    style="color:white"></i></button>
        </div>
        <div class="col-6" id="todo-text-container">
            <h3>{{ data.title }}</h3>
            <p>{{ data.description }}</p>
        </div>
        <div class="col" id="todo-date-container">
            <span>{{ data.fecha }}</span>
        </div>
    </div>
</template>
<script>
export default {
    name: "IndividualTodo",
    props: ["data", "delete", "changeEdit"],
    methods: {
        handleDelete() {
            let resultado = confirm("Estas seguro de eliminar esta tarea?")
            if (resultado === true) {
                this.delete(this.data.id)
            }
        },
        handleEdit(e) {
            let $container = e.target.parentElement.parentNode
            let $text = $container.querySelector("#todo-text-container")
            let tarea = {
                title: $text.querySelector("h3").innerText,
                description: $text.querySelector("p").innerText,
                id: this.data.id
            }
            e.preventDefault()
            this.changeEdit(tarea)
        }
    }
}
</script>

<style>
#individual-todo {
    border: 2px solid white;
    border-radius: 15px;
}

#todo-text-container {
    border-left: 2px solid white;
    padding: 2rem 1rem;
}

#todo-text-container,
#todo-buttons-container {
    border-bottom: 2px solid white;
}

.boton-todo {
    width: 80px;
    height: 60px;
    border-radius: 10px;
    border: none;
}
</style>