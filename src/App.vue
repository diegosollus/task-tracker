<script lang="ts">
  import '@fortawesome/fontawesome-free/css/all.css'
  import 'bulma/css/bulma.min.css'
  import BarraLateral from './components/BarraLateral.vue';
  import FormularioPrincipal from './components/FormularioPrincipal.vue';
  import TarefaObjetivo from './components/TarefaObjetivo.vue';
  import type ITarefa from './interfaces/ITarefa';
  import CardBox from './components/CardBox.vue';

  export default {
    name: 'App',
    components: { BarraLateral, FormularioPrincipal, TarefaObjetivo, CardBox },
    data() {
      return {
        tarefas: [] as ITarefa[],
        modoEscuroAtivo: false
      }
    },
    computed: {
      listaEstaVazia (): boolean {
        return this.tarefas.length === 0
      }
    },
    methods: {
      salvarTarefa(tarefa: ITarefa) {
        this.tarefas.push(tarefa)
      },
      trocarTema(modoEscuroAtivo: boolean) {
        this.modoEscuroAtivo = modoEscuroAtivo
      }
    }
  }
</script>

<template>
  <main class="columns is-gapless is-multiline" :class="{'modo-escuro' : modoEscuroAtivo}">
    <div class="column is-one-quarter">
      <BarraLateral @aoTemaAlterado="trocarTema"/>
    </div>

    <div class="column is-three-quarter conteudo">
      <FormularioPrincipal @aoSalvarTarefa="salvarTarefa"/>
      <div class="lista">
        <TarefaObjetivo v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa" />

        <CardBox v-if="listaEstaVazia">
          Você não está muito produtivo hoje :(
        </CardBox>
      </div>
    </div>
  </main>
</template>

<style scoped>
  .lista {
    padding: 1.25rem;
  }

  main {
    --bg-primario: #fff;
    --texto-primario: #000;
  }

  main.modo-escuro {
    --bg-primario: #2b2d42;
    --texto-primario: #ddd;
  }

  .conteudo {
    background-color: var(--bg-primario);
  }
</style>
