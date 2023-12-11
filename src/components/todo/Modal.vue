<template>
    <section id="modal-container">
        <div id="modal" class="d-flex flex-column justify-content-between align-items-center">
            <template v-if="user_edit">
                <h2>Editar Tarea</h2>
                <form action="" class="w-100" @submit=handleSubmitEdit>
                    <div class="my-2">
                        <label for="title" class="form-label ">Titulo </label>
                        <input type="text" name="title" id="title" :value=user_edit.title class="form-control" required>
                    </div>
                    <div class="my-2">
                        <label for="description" class="form-label">Descripcion</label>
                        <textarea name="description" id="description" cols="10" :value=user_edit.description rows="10"
                            class="form-control" required></textarea>
                    </div>
                    <div class="my-4">
                        <button class="btn btn-primary w-100" type="submit" :data-id=user_edit.id>Editar</button>
                    </div>
                    <i class="fa-solid fa-xmark fa-2xl" @click=handleCloseEdit id="close-modal"></i>
                </form>
            </template>
            <template v-else>
                <h2>Añadir Tarea</h2>
                <form action="" class="w-100" @submit=handleSubmit>
                    <div class="my-2">
                        <label for="title" class="form-label ">Titulo </label>
                        <input type="text" name="title" id="title" class="form-control" required>
                    </div>
                    <div class="my-2">
                        <label for="description" class="form-label">Descripcion</label>
                        <textarea name="description" id="description" cols="10" rows="10" class="form-control"
                            required></textarea>
                    </div>
                    <div class="my-4">
                        <button class="btn btn-primary w-100" type="submit">Añadir</button>
                    </div>
                    <i class="fa-solid fa-xmark fa-2xl" @click=handleClose id="close-modal"></i>
                </form>
            </template>

        </div>
    </section>
</template>
<script>
export default {
    name: "ModalSection",
    props: ["close", "data", "add", "user_edit", "edit", "changeUser"],
    methods: {
        handleClose() {
            this.close()
        }, async handleSubmit(e) {
            let $form = e.target
            let user = {
                title: $form.title.value,
                description: $form.description.value,
                id_user: this.data.id
            }
            e.preventDefault()
            this.add(user)
        }, async handleSubmitEdit(e) {
            let $form = e.target
            let idUser = $form.querySelector("button").dataset.id
            let user = {
                title: $form.title.value,
                description: $form.description.value
            }
            e.preventDefault()
            this.edit(idUser, user)
        }, handleCloseEdit() {
            this.changeUser("")
            this.close()
        }
    }
}
</script>
<style>
#modal-container {
    position: absolute;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: #000000bf;
    display: flex;
    justify-content: center;
    align-items: start;
}

textarea {
    resize: none;
    height: 200px;
}

#modal {
    width: 600px;
    height: 500px;
    background-color: white;
    padding: 1rem 2rem;
    border-radius: 15px;
    color: black;
    margin-top: 10rem;
    position: relative;
}

#app {
    position: relative;
}

#close-modal {
    position: absolute;
    top: 2rem;
    right: 1rem;
    cursor: pointer;
}
</style>