<template>
  <div>
      <div class='row'>
          <div
            class='col-12'
            v-for="pais in paises"
            :key="pais.name"
          >
            <Card :pais="pais" />
          </div>
      </div>
  </div>
</template>

<script>
import Card from './Card';
import { computed, onMounted } from 'vue';
import { useStore } from 'vuex';
export default {
    setup() {
        // para acceder a vuex con setup, solo usa el hook useStore() y directamente tendrás
        // 1.- store.state.paises para acceder al estado global
        // 2.- store.dispatch('getPaises', otroParametro) para ejecutar acciones de vuex
        const store = useStore()

        // Para acceder a un state actualizado debo hacer por propiedad computadas
        // const paises = computed(() => {
        //     return store.state.paises
        // })

        // O podrías usar un getter
        const paises = computed(() => {
            return store.getters.topPaisesPoblacion
        })
        
        onMounted(async () => {
            await store.dispatch('getPaises')
            await store.dispatch('filtrarRegion', 'Americas')
            // console.log('store.state.paises', store.state.paises);
        })

        return {paises}
    },
    components: {
        Card,
    }
}
</script>
