<template>
    <NavBarSection :logout=logout :data=data_user />
    <ToDo :changeModal=changeModal :data=data_user :todos=todos :delete=deleteTodo :changeEdit=changeUserEdit />
    <template v-if="modal === true">
        <ModalSection :close=changeModal :data=data_user :add=addTodo :user_edit=user_edit :edit=editTodo
            :changeUser=changeUserEdit />
    </template>
    <FooterSection />
    <template v-if="loader === true">
        <LoaderComponent />
    </template>
    <template v-if="modalAlert === true">
        <ModalAlert :message=messageModal />
    </template>
</template>

<script>
import NavBarSection from './NavBar.vue';
import FooterSection from './Footer.vue';
import ModalSection from './Modal.vue';
import ToDo from './Todo.vue'
import LoaderComponent from '../LoaderComponent.vue';
import ModalAlert from '../ModalAlert.vue';
export default {
    name: "TodoSection",
    props: ["logout"],
    data() {
        return {
            modal: false,
            data_user: JSON.parse(window.sessionStorage.getItem("user_data")),
            todos: [],
            user_edit: "",
            loader: false,
            modalAlert: false,
            messageModal: ""
        }
    }, components: {
        NavBarSection,
        FooterSection,
        ToDo,
        ModalSection,
        LoaderComponent,
        ModalAlert
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
            this.loader = true
            fetch("http://localhost:5000/todos", options)
                .then(res => {
                    if (res.status === 200) {
                        this.loader = false
                        this.modalAlert = true
                        this.messageModal = "✅ Tarea agregada con exito"
                        setTimeout(() => {
                            window.location.reload()
                        }, 700);

                    }
                })
        }, getTodos(user_id) {
            fetch(`http://localhost:5000/todos/${user_id}`)
                .then(res => res.json())
                .then(data => {
                    console.log(data)
                    this.todos = data
                })
                .catch(err => {
                    console.error(err)
                })
        }, deleteTodo(idTodo) {
            this.loader = true
            let options = {
                method: 'DELETE',
                headers: { 'Content-Type': 'application/json' }
            }
            fetch(`http://localhost:5000/todos/${idTodo}`, options)
                .then(res => {
                    if (res.status === 200) {
                        this.loader = false
                        this.modalAlert = true
                        this.messageModal = "✅ Tarea eliminada correctamente"
                        setTimeout(() => {
                            window.location.reload()
                        }, 700);
                    }
                })
                .catch(err => {
                    console.error(err)
                })
        }, editTodo(idTodo, todo) {
            this.loader = true
            let options = {
                body: JSON.stringify(todo),
                method: 'PUT',
                headers: { 'Content-Type': 'application/json' }
            }
            fetch(`http://localhost:5000/todos/${idTodo}`, options)
                .then(res => {
                    if (res.status === 200) {
                        this.loader = false
                        this.modalAlert = true
                        this.messageModal = "✅ Tarea editada correctamente"
                        setTimeout(() => {
                            window.location.reload()
                        }, 700);
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