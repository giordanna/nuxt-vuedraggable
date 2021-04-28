<template>
  <div class="min-h-screen bg-red-100">
    <div class="max-w-screen-md w-full mx-auto py-16">
      <h1 class="text-3xl my-5 text-center">
        Testando drag n drop
      </h1>
      <draggable
        v-model="secoes"
        :animation="150"
        handle=".handleSecao"
        draggable=".dragSecao"
        class="grid grid-cols-1 gap-y-3"
        @change="atualizaSecoes"
      >
        <section
          class="dragSecao relative p-3 bg-red-200 rounded min-h-custom"
          v-for="secao in secoes"
          :key="secao.name"
        >
          <header class="flex items-center justify-between p-1 mb-3 text-xl">
            <h1>
              {{ secao.name }}
            </h1>
            <button
              class="handleSecao p-1 bg-red-100 rounded-full text-white uppercase text-md"
            >
              🖐️
            </button>
          </header>

          <draggable
            v-model="secao.atributos"
            :animation="150"
            handle=".handle"
            draggable=".drag"
            group="atributos"
            @change="atualizaAtributos(secao.atributos)"
            class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 2xl:grid-cols-5 gap-3 relative"
          >
            <div
              :class="['md:col-span-' + atributo.tamanho]"
              class="col-span-1 drag relative bg-white p-3 text-xl rounded shadow h-24 flex justify-center items-center flex-col z-0 text-center"
              v-for="atributo in secao.atributos"
              :key="atributo.id"
            >
              <button
                class="handle absolute top-1 right-1 p-1 bg-green-100 rounded-full text-white uppercase text-md"
              >
                🖐️
              </button>
              {{ atributo.name }}
            </div>

            <div
              slot="header"
              v-if="secao.atributos.length === 0"
              class="border-dashed opacity-100 hover:opacity-25 absolute border-4 border-black w-full col-span-1 sm:col-span-2 md:col-span-3 lg:col-span-4 2xl:col-span-5  text-xl font-bold uppercase p-3 rounded shadow h-24 flex justify-center items-center flex-col z-0 text-center"
            >
              Arraste aqui seu atributo
            </div>
          </draggable>
        </section>
      </draggable>
    </div>
  </div>
</template>

<script>
let id = 1;
export default {
  data() {
    return {
      secoes: [
        {
          name: "Seção 1",
          ordem: 2,
          atributos: [
            { name: "Atributo 1", id: 0, tamanho: 1, ordem: 2 },
            { name: "Atributo 2", id: 1, tamanho: 2, ordem: 1 },
            { name: "Atributo 3", id: 2, tamanho: 2, ordem: 0 },
            { name: "Atributo 4", id: 3, tamanho: 3, ordem: 3 }
          ]
        },
        {
          name: "Seção 2",
          ordem: 0,
          atributos: [
            { name: "Atributo 5", id: 4, tamanho: 4, ordem: 1 },
            { name: "Atributo 6", id: 5, tamanho: 1, ordem: 2 },
            { name: "Atributo 7", id: 6, tamanho: 5, ordem: 0 }
          ]
        },
        {
          name: "Seção 3",
          ordem: 1,
          atributos: [
            { name: "Atributo 8", id: 7, tamanho: 3, ordem: 0 },
            { name: "Atributo 9", id: 8, tamanho: 2, ordem: 1 },
            { name: "Atributo 10", id: 9, tamanho: 3, ordem: 2 }
          ]
        }
      ]
    };
  },
  mounted() {
    this.secoes.sort((a, b) => a.ordem - b.ordem);
    this.secoes.map(secao => {
      secao.atributos.sort((a, b) => a.ordem - b.ordem);
    });
  },
  methods: {
    atualizaSecoes() {
      this.secoes.map((secao, index) => {
        secao.ordem = index;
      });
    },
    atualizaAtributos(atributos) {
      atributos.map((atributo, index) => {
        atributo.ordem = index;
      });
    }
  }
};
</script>

<style>
.min-h-custom {
  min-height: theme("spacing.44");
}
</style>
