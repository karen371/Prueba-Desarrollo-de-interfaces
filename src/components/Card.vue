<script>
import axios from 'axios';
export default {
    props: { //paso de datos por props
        contadorDescubiertos: { // Recibiendo el contador como prop
            type: Number,
            required: true
        },
        pokemon: {
            type: Object,
            required: true
        }
    },
    data(){
        return{
            imageUrl: '', //url de la imagen obtenida de la api
            nomPokemon: '', //nombre del pokemon que se obtiene del input
            isDiscovered: true, // Cambia esto a true para aplicar la clase
        };
    },
    async mounted(){
        try {
            // Hacemos una solicitud a la URL del Pokémon que recibimos en las props
            const response = await axios.get(this.pokemon.url);
            // Extraemos la URL de la imagen del Pokémon
            this.imageUrl = response.data.sprites.front_default;
        } catch (error) {
            console.error('Error fetching Pokémon data:', error);
        }
    },
    methods:{
        descubrirPokemon(){
            //comparar el nombre del pokémon obtenido en la api con el ingresado
            if(this.pokemon.name.toLowerCase() === this.nomPokemon.toLocaleLowerCase()){
                this.isDiscovered = false; //Se quita la clase descubrir 
                this.$emit('pokemon-descubierto'); // Emitir evento para actualizar el contador
            }
            else{
                alert('Nombre incorrecto, intenta de nuevo'); //mensaje de nombre incorrecto
            }
        }
    },
    computed: {
        nombreFormateado() {
            //Arrglar el formato del nombre para que la primera letra aparezca en mayuscula
            return this.pokemon.name.charAt(0).toUpperCase() + this.pokemon.name.slice(1);
        }
    }
}
</script>
<template>
    <div class="contenedor-card">
        <div class="contenedor-imagen">
            <!--Asignacion de class binding-->
            <img :src="imageUrl" alt="Imagen" :class="{ descubrir: isDiscovered, 'clase-baile': contadorDescubiertos >= 20, 'mover-imagen': contadorDescubiertos >= 20 }" />
        </div>
        <!--Elementos para mostrar u ocultar contenido V-IF-->
        <div class="contenedor-input" v-if="isDiscovered"> 
            <input type="text" placeholder="Nombre del Pokémon" v-model="nomPokemon"  @keyup.enter="descubrirPokemon"/>
            <button @click="descubrirPokemon">Descubrir</button>
        </div>
        <div class="contenedor-input" v-if="!isDiscovered"> 
            <p>{{ nombreFormateado }}</p>
        </div>
    </div>
</template>
<style scoped>
.contenedor-card {
    width: 200px;
    height: 250px;
    border-radius: 10px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2); 
    display: flex;
    flex-direction: column;
    overflow: hidden; 
    background-color: #fff; 
}

.contenedor-imagen {
    width: 100%; 
    height: 60%; 
    display: flex;
    justify-content: center; 
    align-items: center; 
}

.contenedor-imagen img {
    max-width: 150%; 
    max-height: 100%; 
    object-fit: cover;
}

.clase-baile{
    /* Estilos para la imagen cuando el contador llegue a 20 */
    transform: scale(1.1); /* Ejemplo de escalar la imagen */
}
@keyframes mover {
    0% { transform: translateX(0) rotate(0deg); }
    25% { transform: translateX(10px) rotate(5deg); } /* Desplazamiento a la derecha y rotación */
    50% { transform: translateX(-10px) rotate(-5deg); } /* Desplazamiento a la izquierda y rotación */
    75% { transform: translateX(10px) rotate(5deg); } /* Regresar a la posición original */
    100% { transform: translateX(0) rotate(0deg); } /* Volver a la posición original */
}

.mover-imagen {
    animation: mover 1s infinite; /* Cambia el tiempo y la cantidad de repeticiones como desees */
}

.descubrir{
    /*filter: brightness(0) grayscale(100%);*/
    filter: blur(5px) grayscale(100%);
}

.contenedor-input {
    width: 100%; 
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 10px 0;
}

input[type="text"] {
    width: 80%; 
    padding: 5px; 
    border: 1px solid #ccc; 
    border-radius: 5px; 
    margin-bottom: 10px; 
}

button {
    background-color: #e64a19; 
    color: white; 
    border: none; 
    border-radius: 5px; 
    padding: 10px; 
    cursor: pointer;
    transition: background-color 0.3s; 
}

button:hover {
    background-color: #d84315; 
}
</style>
