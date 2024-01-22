<template>
    <div
        class="is-flex is-align-items-center is-justify-content-space-between"
    >
        <CronometroTempo :segundos="segundos"/>
        <button class="button" @click="iniciar" :disabled="cronometroRodando">
        <span class="icon">
            <i class="fas fa-play"></i>
        </span>
        <span>Play</span>
        </button>
        <button class="button" @click="finalizar" :disabled="!cronometroRodando">
        <span class="icon">
            <i class="fas fa-stop"></i>
        </span>
        <span>Stop</span>
        </button>
    </div>
</template>

<script lang="ts">
    import { defineComponent } from 'vue'
    import CronometroTempo from './CronometroTempo.vue';

    export default defineComponent({
        name: 'TemporizadorTarefa',
        emits: ['aoTemporizadorFinalizado'],
        components: { CronometroTempo },
        data() {
            return {
                segundos: 0,
                cronometro: 0,
                cronometroRodando: false,
            };
        },
        methods: {
            iniciar() {
                this.cronometroRodando = true
                this.cronometro = setInterval(() => {
                    this.segundos += 1;
                }, 1000);
            },
            finalizar() {
                this.cronometroRodando = false
                clearInterval(this.cronometro);
                this.$emit('aoTemporizadorFinalizado', this.segundos)
                this.segundos = 0
            }
        },
        computed: {
            tempoDecorrido(): string {
                return new Date(this.segundos * 1000).toISOString().slice(11, 19);
            }
        },
    })
</script>   