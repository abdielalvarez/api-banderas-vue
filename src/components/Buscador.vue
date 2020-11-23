<template>
    <div>
        <!-- @keyup ejecuta un metodo al dejar de presionar una tecla -->
        <!-- la intención es ejecutar una busqueda por string -->
        <input
            text="text"
            placeholder="Ingrese País"
            class="form-control my-3"
            v-model="texto"
            @keyup="procesarInput"
        >
    </div>
</template>

<script>
import { ref } from 'vue'
import { useStore } from 'vuex'
export default {
    setup() {
        const texto = ref('')
        const store = useStore()

        const procesarInput = () => {
            // console.log('texto.value', texto.value);
            store.dispatch('filtrarNombre', texto.value)
        }

        return {texto, procesarInput}
    }
}
</script>
