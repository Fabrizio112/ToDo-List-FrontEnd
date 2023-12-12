<template>
    <div>
        <h1 class="mb-4 mt-2 fs-2 ">Iniciar Sesion</h1>
        <form action="" class="gap-4 d-flex flex-column" @submit="handleLogin">
            <div>
                <input type="email" placeholder="Correo Electronico" name="email" class="form-control py-2" required>
            </div>
            <div>
                <input type="password" placeholder="Contraseña" name="password" class="form-control py-2" required>
            </div>
            <button class="btn btn-dark btn-lg">Iniciar Sesion</button>
        </form>
    </div>
</template>


<script>
export default {
    name: "IniciarSesion",
    props: ["login"],
    methods: {
        handleLogin(e) {
            e.preventDefault()
            let $form = e.target
            let usuarioFinal = {
                email: $form.email.value,
                password: $form.password.value
            }
            this.login(usuarioFinal)
        }
    }
}

</script>