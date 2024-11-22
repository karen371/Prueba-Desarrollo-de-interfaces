<script>
import logo from '../assets/pokemon-logo.png'
export default {
    data() {
        return {
            logo, // Puedes almacenar la imagen aquí
        };
    },
};

</script>
<template>
    <header>
        <div class="contenedor-imagen">
            <img :src="logo" alt="logo de pokemon">
        </div>
        <div class="contenedor-titulo">
            <h1>¿Quién es ese Pokémon?</h1>
        </div>
    </header>
</template>
<style scoped>
    header{
        width: 100%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        margin: 20px 0;
    }
    .contenedor-imagen{
        display: flex;
        justify-content: center;
    }
    .contenedor-imagen img{
        width: 20%;
    }
    .contenedor-titulo h1{
        font-weight: 700;
        font-style: normal;
        font-size: 2rem;
    }
</style>

