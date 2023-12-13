<template>
    <section id="loader-container">
        <div class="spinner-border text-light" role="status">
            <span class="visually-hidden">Loading...</span>
        </div>
    </section>
</template>

<script>
export default {
    name: "LoaderComponent"
}
</script>
<style>
#loader-container {
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

#loader-container div {
    width: 100px;
    height: 100px;
}
</style>