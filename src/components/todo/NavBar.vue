<template>
    <nav class="d-flex justify-content-between aling-items-center ">
        <div id="nav-title" class="d-flex justify-content-center gap-5 align-items-center">
            <img src="../../../public/nota.png" alt="notas">
            <h1 class="display-4 fw-bolder">To-Do App</h1>
        </div>
        <div id="nav-user" class="d-flex justify-content-between align-items-center gap-4">
            <div id="nav-user-avatar">
            </div>
            <div id="nav-user-info">
                <h2 class="fs-5 d-flex gap-2">Hola <p>{{ data ? data.name : "" }}</p>!! </h2>
                <p>@{{ data ? data.username : "" }}</p>
                <div class="mt-2 w-100"><button class="btn btn-danger w-100" @click=handleDelete>Cerrar Sesion</button>
                </div>
            </div>

        </div>
    </nav>
</template>

<style>
nav {
    height: 20vh;
    padding: 0.6rem 1.5rem;
    border-bottom: 3px solid white;
}

#nav-title {
    width: 75%;
}

#nav-title img {
    height: 100%;
}

#nav-user {
    width: 25%;
}

#nav-user p {
    margin: 0;
}

#nav-user-info {
    width: 60%;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: start;
    justify-content: center;
}

#nav-user-avatar {
    width: 40%;
    height: 100%;
    border-radius: 15px;
    background-image: url("../../../public/default\ image.webp");
    background-size: cover;
    background-position: center;
}
</style>


<script>
export default {
    name: "NavBarSection",
    props: ["logout", "data"],
    methods: {
        handleDelete() {
            let confirmacionUsuario = confirm("Estas seguro de Cerrar Sesion?")
            if (confirmacionUsuario === true) {
                setTimeout(() => {
                    this.logout()
                }, 200);
            }

        }
    }
}
</script>