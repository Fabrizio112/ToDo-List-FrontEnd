<template>
    <nav class="d-flex justify-content-between aling-items-center ">
        <div id="nav-title" class="d-flex justify-content-center align-items-center">
            <h1 class="display-4">To-Do App</h1>
        </div>
        <div id="nav-user" class="d-flex justify-content-between align-items-center gap-4">
            <div id="nav-user-avatar">
            </div>
            <div id="nav-user-info">
                <p>{{ data ? data.name : "" }}</p>
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
    name: "NavBar",
    props: ["logout", "data"],
    methods: {
        handleDelete() {
            this.logout()
        }
    }
}
</script>