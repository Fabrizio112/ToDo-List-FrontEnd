<template>
    <template v-if="loader === true">
        <LoaderComponent />
    </template>

    <div>
        <h1 class="mb-4 mt-2 fs-2 ">Iniciar Sesion</h1>
        <form action="" class="gap-4 d-flex flex-column" @submit="handleLogin">
            <div class="alert alert-danger" role="alert" v-if="error === true">
                <span>❌ Email o Contraseña incorrectos</span>
            </div>
            <div>
                <input type="email" placeholder="Correo Electronico" name="email" class="form-control py-2"
                    @keyup=handleValidate required>
            </div>
            <div>
                <input type="password" placeholder="Contraseña" name="password" class="form-control py-2"
                    @keyup=handleValidate required>
            </div>
            <button class="btn btn-dark btn-lg">Iniciar Sesion</button>
        </form>
    </div>
    <template v-if="modal === true">
        <ModalAlert message="😊 Inicio de Sesion Exitoso" />
    </template>
</template>


<script>
import LoaderComponent from '../LoaderComponent.vue'
import ModalAlert from '../ModalAlert.vue'



export default {
    name: "IniciarSesion",
    props: ["login", "error", "loader", "modal"],
    methods: {
        handleLogin(e) {
            e.preventDefault()
            let $form = e.target
            let usuarioFinal = {
                email: $form.email.value,
                password: $form.password.value
            }
            this.login(usuarioFinal)
        }, handleValidate(e) {
            console.log(e.target.value)
        }
    },
    components: {
        LoaderComponent,
        ModalAlert
    }
}

</script>