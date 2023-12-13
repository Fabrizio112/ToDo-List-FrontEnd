<template>
    <template v-if="loader === true">
        <LoaderComponent />
    </template>
    <template v-if="modal === true">
        <ModalAlert :message=mensaje />
    </template>
    <div id="form-register" class="mt-5">
        <h1 class="mb-4 mt-2 fs-2 ">Crea una cuenta</h1>
        <form action="" class="gap-4 d-flex flex-column" @submit="handleRegister">
            <div class="row">
                <div class="col">
                    <input type="text" placeholder="Nombre" name="name" class="form-control py-2" @keyup=handleVerify
                        title="No puede estar vacio" required>
                    <p v-if="error.nombre.length > 0" class="text-danger w-100 text-start mt-2">❌ {{ error.nombre }}</p>
                </div>
                <div class="col">
                    <input type="text" placeholder="Nombre de Usuario" name="username" class="form-control py-2"
                        title="Usuario Invalido" pattern="^[A-Za-z0-9_\-.]+$" @keyup=handleVerify required>
                    <p v-if="error.username.length > 0" class="text-danger w-100 text-start mt-2">❌ {{ error.username }}</p>
                </div>
            </div>
            <div>
                <input type="email" placeholder="Correo Electronico" name="email" class="form-control py-2"
                    pattern="^[^@]+@[^@]+\.[a-zA-Z]{2,}$" title="Email incorrecto" @keyup=handleVerify required>
                <p v-if="error.email.length > 0" class="text-danger w-100 text-start mt-2">❌ {{ error.email }}</p>
            </div>
            <div>
                <input type="password" placeholder="Contraseña" name="password" class="form-control py-2"
                    @keyup=handlePassword required>
            </div>
            <div>
                <input type="password" placeholder="Repetir Contraseña" name="r-password" class="form-control py-2"
                    @keyup=handleVerify required>
                <p v-if="error.password.length > 0" class="text-danger w-100 text-start mt-2">❌ {{ error.password }}</p>
            </div>
            <button class="btn btn-dark btn-lg">Dar de alta</button>
        </form>
    </div>
    <template>

    </template>
</template>
<script>
import LoaderComponent from '../LoaderComponent.vue'
import ModalAlert from '../ModalAlert.vue';

export default {
    name: "LoginForm",
    props: ["registrar", "loader", "modal", "mensaje"],
    data() {
        return {
            error: {
                nombre: "",
                username: "",
                email: "",
                password: ""
            },
            password: ""
        };
    },
    methods: {
        handleRegister(e) {
            e.preventDefault();
            let $form = e.target;
            let usuarioFinal = {
                name: $form.name.value,
                username: $form.username.value,
                email: $form.email.value,
                password: $form.password.value
            };
            this.registrar(usuarioFinal);
        }, handlePassword(e) {
            this.password = e.target.value;
        },
        handleVerify(e) {
            if (e.target.name === "name") {
                e.target.validity.valid === false ? this.error.nombre = e.target.title : this.error.nombre = "";
            }
            else if (e.target.name === "username") {
                e.target.validity.valid === false ? this.error.username = e.target.title : this.error.username = "";
            }
            else if (e.target.name === "email") {
                console.log(e.target.validity.valid);
                e.target.validity.valid === false ? this.error.email = e.target.title : this.error.email = "";
            }
            else if (e.target.name === "r-password") {
                e.target.value != this.password ? this.error.password = "Las constraseñas no coinciden" : this.error.password = "";
            }
        }
    },
    components: { LoaderComponent, ModalAlert }
}

</script>

<style>
#form-register {
    height: 80%;
}

#form-register form div div p,
#form-register form div p {
    margin: 0;
}
</style>