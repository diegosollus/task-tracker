
import CronometroTempo from './CronometroTempo.vue';
<template>
    <CardBox>
        <div class="columns">
            <div class="column is-7">
                {{ tarefa.descricao || 'Tarefa sem descrição' }}
            </div>

            <div class="column">
                <CronometroTempo :segundos="tarefa.duracaoEmsegundos" />
            </div>
        </div>
    </CardBox>
</template>

<script lang="ts">
    import type { PropType } from 'vue';
    import CronometroTempo from './CronometroTempo.vue';
    import type ITarefa from '@/interfaces/ITarefa';
    import CardBox from './CardBox.vue';

    export default{
        name: 'TarefaObjetivo',
        components: { CronometroTempo, CardBox },
        props: {
            tarefa: {type: Object as PropType<ITarefa>, required: true}
        }
    }
</script>