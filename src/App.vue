<template>
  <template v-if="login === 'true'">
    <TodoSection :logout=cerrarSesion />
  </template>
  <template v-else>
    <LoginSection :actualizar_login=actualizarLogin :data=obtenerInformacionUsuario />
  </template>
</template>

<script>
import LoginSection from '../src/components/login/LoginSection.vue'
import TodoSection from './components/todo/TodoSection.vue'


export default {
  name: 'App',
  data() {
    return {
      login: window.sessionStorage.getItem("login") ? window.sessionStorage.getItem("login") : false
    }
  },
  components: {
    LoginSection,
    TodoSection
  }, methods: {
    actualizarLogin() {
      this.login = window.sessionStorage.getItem("login")
    },
    cerrarSesion() {
      window.sessionStorage.setItem("login", false)
      this.login = window.sessionStorage.getItem("login")
    }, async obtenerInformacionUsuario(email) {
      try {
        let response = await fetch(`http://localhost:5000/users/${email}`)
        let data = await response.json()
        window.sessionStorage.setItem("user_data", JSON.stringify(data))
      } catch (error) {
        console.error(error)
      }
    }
  }
}
</script>

<style>
#app {
  font-family: "Roboto Condensed", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
}
</style>
