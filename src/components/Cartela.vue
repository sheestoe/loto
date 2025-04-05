<script setup>
defineProps(['numbers', 'title', "disableArray"])
const selected = defineModel({default: []})
</script>

<template>
<!-- https://codepen.io/scorpionvv/pen/eYZrooJ -->
<div class="lotoBg">
    <h3 class="title">
    {{title}}
    </h3>
    <label v-for="n in numbers">
      <input type="checkbox" :value="n" v-model="selected" :disabled="disableArray?.includes(n)">
      <span>{{String(n).padStart(2, '0')}}</span>
    </label>
</div>
</template>

<style scoped>
label {
  cursor: pointer;
  flex-basis: 20%;
}

label [type="checkbox"] {
  display: none;
}

[type="checkbox"]+span {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2px;
  border-style: solid;
  border-width: 1px;
  border-color: purple;
  background-color: #FFFFFF;
  border-radius: 3px;
  margin: 1em 0.5em;
}

:checked+span {
  display: flex;
  text-shadow: 0.5px 0px 0px #555, -0.5px 0px 0px #555;
  background-color: #B5C9DF !important;
}

[type="checkbox"][disabled]+span {
  background-color: #c4c4c4 !important;
  color: #555;
  border-color: #555;
}

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