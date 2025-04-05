<script setup>
import { watch } from 'vue'
  const props = defineProps({
    title: String,
    minDezenas: {
      type: Number,
      default: 1
    },
    maxDezenas: {
      type: Number,
      default: 25
    }
  })
  const numDezenas = ref(15)
  const numJogos = ref(5)

  watch(
    () => props.minDezenas,
    (newValue, oldValue) => {
      if (numDezenas.value < newValue) {
        numDezenas.value = newValue
      }
    }
  );

  watch(
    () => props.maxDezenas,
    (newValue, oldValue) => {
      if (numDezenas.value > newValue) {
        numDezenas.value = newValue
      }
    }
  );
</script>

<template>
  <div class="lotoBg">
    <v-container>
      <v-row>
        <v-col>
          <h3 class="title">
            {{title}}
          </h3>
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <h5>Quantas jogos?</h5>
          <v-number-input v-model="numJogos" control-variant="split" :min="1" :step="5"></v-number-input>
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <h5>Quantas dezenas?</h5>
          <v-number-input v-model="numDezenas" control-variant="split" :max="maxDezenas" :min="minDezenas"></v-number-input>
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <v-btn class="text-none" append-icon="mdi-chevron-right-circle-outline" variant="text" border @click="$emit('generate', numDezenas, numJogos)">
            Gerar
          </v-btn>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<style scoped>
.lotoBg {
    display: flex;
    justify-content: space-between;
    flex-flow: row wrap;
    border-style: solid;
    border-width: 1px;
    border-color: purple;
    text-align: center;
    font-size: 12px;
    font-family: arial, verdana;
    color: purple;
    border-radius: 10px;
    box-shadow: 2px 2px 10px -2px #B5B5B5; 
    background-color: #FFFFCE;
}

.title{
    flex-basis: 100%;
}
</style>