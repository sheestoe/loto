<script setup>
  const totalNumbers = 25;
  const numbers =  shallowRef(Array.from({ length: totalNumbers }, (_, i) => i + 1));
  const toRemove = shallowRef([])
  const toKeep = shallowRef([])
  const results = shallowRef([])
  const dialog = ref(false)

  const g = (maxSize) => {
    maxSize = maxSize - toKeep.value.length
    if (!numbers.value || !toRemove.value || !toKeep.value){
      return;
    }
    const array = numbers.value.filter(function (el) {
      return !toRemove.value.includes(el) && !toKeep.value.includes(el);
    });

    const result = [];
    const currentCombination = [];

    function generateCombinations(start, currentSize) {
      if (currentSize === 0) {
        currentCombination
        result.push([...currentCombination.concat(toKeep.value).map((n) => (`${n}`.padStart(2, '0'))).sort()]);
        return;
      }

      for (let i = start; i < array.length; i++) {
        currentCombination.push(array[i]);
        generateCombinations(i + 1, currentSize - 1);
        currentCombination.pop();
      }
    }

    generateCombinations(0, maxSize);
    return result;
  }

  function generate(numDezenas, numJogos){
    const list = g(numDezenas)
    let shuffled = list
    .map(value => ({ value, sort: Math.random() }))
    .sort((a, b) => a.sort - b.sort)
    .map(({ value }) => value)
    results.value = shuffled.slice(0, numJogos)
    dialog.value = true
  }
</script>

<template>
  <v-main>
    <div class="main">
      <Cartela :numbers=numbers title="Garantir" class="cartela" :disableArray="toRemove" v-model="toKeep"/>
      <Cartela :numbers=numbers title="Eliminar" class="cartela" :disableArray="toKeep" v-model="toRemove"/>
      <Params title="Gerar" class="cartela" :maxDezenas="numbers.length - toRemove.length" :minDezenas="toKeep.length + 1" @generate="generate" />
      <v-dialog
        v-model="dialog"
        width="auto"
      >
        <v-card
          prepend-icon="mdi-currency-usd"
          title="Resultados"
          class="dialog"
        >
          <div id="result-ct" v-for="row in results">
            <span class="circle" v-for="n in row">
              {{n}}
            </span>
          </div>
          <template v-slot:actions>
            <v-btn
              class="ms-auto"
              text="Ok"
              @click="dialog = false"
            ></v-btn>
          </template>
        </v-card>
      </v-dialog>
    </div>
  </v-main>
</template>

<style scoped>
.main{
  align-self: stretch;
  display: flex;
  flex-direction: row;
}
.cartela{
  flex-basis: 30%;
  margin: 1em;
}
#result-ct {
    padding: 3px;
}

.circle {
    line-height: 26px;
    border-radius: 50%;
    -moz-border-radius: 50%;
    -webkit-border-radius: 50%;
    border: 1px solid #a4508c;
    text-align: center;
    color: #282828;
    font-family: "Trebuchet MS", Arial, Helvetica, sans-serif;
    font-size: 13.5px;
    font-weight: 700;
    margin: 3px;
    display: inline-block;
    background-color: #ede1e8;
    padding: 2px 5.5px
}
.dialog{
  padding: 10px;
  margin: 10px;
}
</style>
