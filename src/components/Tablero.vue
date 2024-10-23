<script>
import logo from '../assets/pokemon-logo.png'
import Card from './Card.vue';

export default {
    data() {
        return {
            pokemones: [], // Aquí tendrás que cargar tu lista de Pokémon
            contadorDescubiertos: 0, // Contador de Pokémon descubiertos
        };
    }, //paso de datos por props
    props: {
        pokemon: {
            type: Array,
            required: true
        }
    },
    methods: {
        //metodo para aumetar el contador de pokémon
        aumentarContador() {
            this.contadorDescubiertos++; 
            if(this.contadorDescubiertos == 20){
                alert('¡Felicidades, has descubierto todos los Pokémon!');
            }
        }
    },
    components: {
        logo,
        Card
    }
}
</script>
<template>
    <section class="contenedor-tablero">
        <div class="encabezado-tablero">
            <h4>Pokemones descubiertos: <span class="contador">{{ contadorDescubiertos }}</span></h4>
        </div>
        <div class="tablero">
            <!--reutilizacion de componentes-->
            <Card 
                v-for="pokemones in pokemon" 
                :key="pokemones.name" 
                :pokemon="pokemones" 
                @pokemon-descubierto="aumentarContador"
            />
        </div>
    </section>
</template>
<style scoped>
.contenedor-tablero {
    display: flex;
    flex-direction: column;
    border-radius: 10px; 
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2); 
    padding: 10px; 
    background-color: #fff; 
    margin: 20px;
}

.contador{
    color: orangered;
    font-size: 1.2rem;
}

.encabezado-tablero {
    text-align: center;
    padding: 10px; 
}

.tablero {
    display: grid;
    grid-template-columns: repeat(5, 1fr); 
    grid-template-rows: repeat(5, auto); 
    gap: 30px; 
    padding: 10px; 
    margin: auto;
}
</style>
