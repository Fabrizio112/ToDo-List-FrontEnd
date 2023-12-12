<template>
    <main id="main-login" class="w-100 d-flex justify-content-center align-items-center">
        <div id="login-container" class="d-flex">
            <section id="login-container-img">
                <template v-if="botonClickeado === 'Iniciar Sesion'">
                    <img src="../../../public/login.jpg" alt="photo login">
                </template>
                <template v-else>
                    <img src="../../../public/register.jpg" alt="photo register">
                </template>
            </section>

            <section id="login-container-content">
                <section id="logo-section" class="d-flex gap-3">
                    <img src="../../../public/nota.png" alt="">
                    <h1>To Do App</h1>
                </section>
                <section id="content-section" class="d-flex flex-column justify-content-around">
                    <div v-if="botonClickeado === 'Iniciar Sesion'">
                        <IniciarSesion :login=loginUser />
                    </div>
                    <div v-else>
                        <Registrarse :registrar=signUpUser />
                    </div>
                    <section v-if="botonClickeado === 'Iniciar Sesion'">
                        <p>No tienes una cuenta? <button @click="handleChangeBoton" class="boton-login">Registrarse</button>
                        </p>
                    </section>
                    <section v-else>
                        <p>Ya tienes una cuenta? <button @click="handleChangeBoton" class="boton-login">Iniciar
                                Sesion</button></p>
                    </section>
                </section>

            </section>


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

#logo-section img {
    width: 50px;
    height: 50px;

}

#logo-section {
    height: 10%;
}

#content-section {
    height: 90%;
}

#login-container {
    width: 90%;
    height: 600px;
    border-radius: 15px;
    color: black;
    background-color: white;
}

#login-container-img,
#login-container-content {
    width: 50%;
    height: 100%;
}

#login-container-img img {
    height: 100%;
    width: 100%;
    object-fit: cover;
    border-top-left-radius: 15px;
    border-bottom-left-radius: 15px;
}

#login-container-content {
    padding: 2rem;
}

#section-buttons {
    height: 20%;
}

.boton-login {
    background-color: transparent;
    border: none;
    font-weight: 900;
    cursor: pointer;
}
</style>