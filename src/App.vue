<script setup>
import { ref } from 'vue'
import KnappRad from './components/KnappRad.vue'
import ResultatRad from './components/ResultatRad.vue'
import PoangRad from './components/PoangRad.vue'

const resultat = ref('Lets Begin!')
const knappar = ref(['Sten', 'Sax', 'Påse', 'Lizard', 'Spock'])
const vinnare = ref('')
const reset = ref(true)

function hittaVinnare(valdaKnappar) {
  reset.value = false
  vinnare.value = ''
  let spelare = knappar.value.indexOf(valdaKnappar.spelare)
  let dator = knappar.value.indexOf(valdaKnappar.dator)
  resultat.value = { spelare: spelare, dator: dator }
}

function raknaPoeng(v) {
  vinnare.value = v
}
</script>

<template>
  <header>
    <h1>Sten, Sax, Påse!</h1>
  </header>

  <main>
    <KnappRad :knappar="knappar" :reset="reset" @valdaKnappar="hittaVinnare" />
    <ResultatRad :valda-knappar="resultat" :reset="reset" @vinnare="raknaPoeng" />
    <PoangRad :vinnare="vinnare" :reset="reset" />
    <div class="Score">
      <button id="nolla" @click="reset = true">Nollställ poängen</button>
    </div>
  </main>
</template>

<style scoped>
header {
  text-align: center;
  margin-bottom: 1.2em;
}

.Score {
  font-size: 1.2em;
  text-align: center;
}
#nolla {
  margin-top: 2em;
  padding: 0.3em 0.6em;
  font-size: 0.8em;
}
button {
  padding: 0.6em 1.2em;
  font-size: 1.2em;
  background-color: #f0f0f0;
  border: 1px solid #ccc;
  border-radius: 5px;
  cursor: pointer;
}
.knapprad {
  display: flex;
  justify-content: center;
  gap: 0.6em;
}

button.spelarval {
  background-color: greenyellow;
}
button.datorval {
  border: red solid 2px;
}
.resultat {
  font-size: 1.2em;
  text-align: center;
  margin: 1.2em 0;
}
</style>
