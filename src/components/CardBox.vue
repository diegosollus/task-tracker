<template>
    <div class="box has-text-weight-bold" :style="estilos">
        <slot></slot>
    </div>
</template>

<script lang="ts">
    export default{
        name: 'CardBox',
        data() {
            return {
                estilos: {
                    background: '#FAF0CA'
                }
            }
        }
    }
</script>