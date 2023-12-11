<template>
    <main id="main-login" class="w-100 d-flex justify-content-center align-items-center">
        <div id="login-container">
            <section class="d-flex justify-content-center align-items-center gap-2 " id="section-buttons">
                <button class="btn btn-primary w-100 py-2" @click="handleChangeBoton">Iniciar Sesion</button>
                <button class="btn btn-dark w-100 py-2" @click="handleChangeBoton">Registrarse</button>
            </section>
            <div v-if="botonClickeado === 'Iniciar Sesion'">
                <IniciarSesion :login=loginUser />
            </div>
            <div v-else>
                <Registrarse :registrar=signUpUser />
            </div>

        </div>
    </main>
</template>

<script>
import Registrarse from './Registrarse.vue';
import IniciarSesion from './IniciarSesion.vue'
export default {
    name: "LoginForm",
    props: ["actualizar_login", "data"],
    data() {
        return {
            botonClickeado: "Iniciar Sesion",
            urlSignUp: "https://fabrizioavila1.pythonanywhere.com/signup",
            urlLogin: "https://fabrizioavila1.pythonanywhere.com/login",
        }
    },
    components: {
        Registrarse,
        IniciarSesion
    },
    methods: {
        handleChangeBoton(e) {
            this.botonClickeado = e.target.innerText
        },
        signUpUser(user) {
            let options = {
                body: JSON.stringify(user),
                method: 'POST',
                headers: { 'Content-Type': 'application/json' }
            }
            fetch(this.urlSignUp, options)
                .then(response => {
                    if (response.status === 401) {
                        alert("Correo Electronico ya en uso")
                    } else if (response.status === 200) {
                        alert("Usuario Registrado Correctamente")
                        this.botonClickeado = "Iniciar Sesion"
                    }
                })

                .catch(error => {
                    console.error(error)
                })
        },
        async loginUser(user) {
            let options = {
                body: JSON.stringify(user),
                method: 'POST',
                headers: { 'Content-Type': 'application/json' }
            }
            try {
                let response = await fetch(this.urlLogin, options)
                if (response.status === 401) {
                    alert("Correo Electrónico o Contraseña incorrectos")
                } else if (response.status === 200) {
                    alert("Inicio de Sesion Exitoso")
                    window.sessionStorage.setItem("login", true)
                    await this.data(user.email)
                    this.actualizar_login()
                }
            } catch (error) {
                console.error(error)
            }
        }
    }
}

</script>

<style>
#app {
    background-image: linear-gradient(rgba(0, 0, 0, 0.6), rgba(0, 0, 0, 0.6)), url("../../../public/fondo.jpg");
    background-repeat: no-repeat;
    background-size: cover;
    background-color: black;
}


#main-login {
    min-height: 100vh;
}

#login-container {
    width: 500px;
    height: 450px;
    border-radius: 15px;
    color: white;
    padding: 2rem;
    background-color: #ffffff54;
}

#section-buttons {
    height: 20%;
}
</style>