<template>
    <NavBarSection :logout=logout :data=data_user />
    <ToDo :changeModal=changeModal :data=data_user :todos=todos :delete=deleteTodo :changeEdit=changeUserEdit />
    <template v-if="modal === true">
        <ModalSection :close=changeModal :data=data_user :add=addTodo :user_edit=user_edit :edit=editTodo
            :changeUser=changeUserEdit />
    </template>
    <FooterSection />
</template>

<script>
import NavBarSection from './NavBar.vue';
import FooterSection from './Footer.vue';
import ModalSection from './Modal.vue';
import ToDo from './Todo.vue'
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
        NavBarSection,
        FooterSection,
        ToDo,
        ModalSection
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