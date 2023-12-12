<template>
    <nav class="d-flex justify-content-between aling-items-center ">
        <div id="nav-title" class="d-flex justify-content-center gap-5 align-items-center">
            <img src="../../../public/nota.png" alt="notas">
            <h1 class="display-4">To-Do App</h1>
        </div>
        <div id="nav-user" class="d-flex justify-content-between align-items-center gap-4">
            <div id="nav-user-avatar">
            </div>
            <div id="nav-user-info">
                <h2 class="fs-5 d-flex gap-2">Hola <p>{{ data ? data.name : "" }}</p>!! </h2>
                <p>@{{ data ? data.username : "" }}</p>
                <div><button class="btn btn-danger" @click=handleDelete>Cerrar Sesion</button></div>
            </div>

        </div>
    </nav>
</template>

<style>
nav {
    height: 20vh;
    padding: 1rem 1.5rem;
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
    background-image: url("https://via.placeholder.com/100x100.png/a59090/000000?Text=100x100");
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
            this.logout()
        }
    }
}
</script>