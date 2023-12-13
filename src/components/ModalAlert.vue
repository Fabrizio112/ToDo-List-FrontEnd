<template>
    <section id="modal-container-alert">
        <div id="modal-alert">
            <h1>{{ message }}</h1>
        </div>
    </section>
</template>

<script>
export default {
    name: "ModalAlert",
    props: ["message"]
}
</script>

<style>
#modal-container-alert {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #00000066;
}

#modal-alert {
    width: 600px;
    height: 200px;
    background-color: white;
    border-radius: 10px;
    display: flex;
    justify-content: center;
    align-items: center;
    color: black;
}
</style>