<template>
    <div id="footer">
        <p>Blog Lorem &copy; 2023 <br>Desenvolvido por Jaqueline Alencar</p>
    </div>
</template>

<script>
export default {
    name: "Footer"
}
</script>


<style scoped>
#footer {
    height: 200px;
    background-color: black;
    border-top: 4px solid #111;
    color: aliceblue;
    display: flex;
    align-items: center;
    justify-content: center;
    bottom: 0;
    position: static;
    width: 100%;
}
</style>