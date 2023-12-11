<template>
    <NavBar :logout=logout :data=data_user />
    <Todo :changeModal=changeModal :data=data_user :todos=todos :delete=deleteTodo :changeEdit=changeUserEdit />
    <template v-if="modal === true">
        <Modal :close=changeModal :data=data_user :add=addTodo :user_edit=user_edit :edit=editTodo
            :changeUser=changeUserEdit />
    </template>
    <Footer />
</template>

<script>
import NavBar from './NavBar.vue';
import Footer from './Footer.vue';
import Modal from './Modal.vue';
import Todo from './Todo.vue'
export default {
    name: "TodoSection",
    props: ["logout"],
    data() {
        return {
            modal: false,
            data_user: JSON.parse(window.sessionStorage.getItem("user_data")),
            todos: [],
            user_edit: ""
        }
    }, components: {
        NavBar,
        Footer,
        Todo,
        Modal
    },
    methods: {
        changeModal() {
            if (this.modal === true) {
                this.modal = false
            } else if (this.modal === false) {
                this.modal = true
            }
        }, addTodo(user) {
            let options = {
                body: JSON.stringify(user),
                method: 'POST',
                headers: { 'Content-Type': 'application/json' }
            }
            fetch("https://fabrizioavila1.pythonanywhere.com/todos", options)
                .then(res => {
                    if (res.status === 200) {
                        alert("Tarea agregada con exito")
                        window.location.reload()
                    }
                })
        }, getTodos(user_id) {
            fetch(`https://fabrizioavila1.pythonanywhere.com/todos/${user_id}`)
                .then(res => res.json())
                .then(data => {
                    console.log(data)
                    this.todos = data
                })
                .catch(err => {
                    console.error(err)
                })
        }, deleteTodo(idTodo) {
            let options = {
                method: 'DELETE',
                headers: { 'Content-Type': 'application/json' }
            }
            fetch(`https://fabrizioavila1.pythonanywhere.com/todos/${idTodo}`, options)
                .then(res => {
                    if (res.status === 200) {
                        alert("Tarea eliminada correctamente")
                        window.location.reload()
                    }
                })
                .catch(err => {
                    console.error(err)
                })
        }, editTodo(idTodo, todo) {
            let options = {
                body: JSON.stringify(todo),
                method: 'PUT',
                headers: { 'Content-Type': 'application/json' }
            }
            fetch(`https://fabrizioavila1.pythonanywhere.com/todos/${idTodo}`, options)
                .then(res => {
                    if (res.status === 200) {
                        alert("Tarea editada correctamente")
                        window.location.reload()
                    }
                })
                .catch(err => {
                    console.error(err)
                })
        }, changeUserEdit(valor) {
            this.user_edit = valor
            this.modal = true
        }
    }, mounted() {
        this.getTodos(this.data_user.id)
    }
}
</script>

<style></style>