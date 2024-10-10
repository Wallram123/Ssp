<script setup>
import { ref } from 'vue'
import KnappRad from './components/KnappRad.vue'
import ResultatRad from './components/ResultatRad.vue'
import PoangRad from './components/PoangRad.vue'

const score = ref({ spelare: 0, dator: 0 })
const resultat = ref('Lets Begin!')
const knappar = ref(['Sten', 'Sax', 'Påse', 'Lizard', 'Spock'])
const vinnare = ref('')

function hittaVinnare(valdaKnappar) {
  vinnare.value = ''
  let spelare = knappar.value.indexOf(valdaKnappar.spelare)
  let dator = knappar.value.indexOf(valdaKnappar.dator)
  resultat.value = { spelare: spelare, dator: dator }
}
function reset() {
  score.value.spelare = 0
  score.value.dator = 0
  let buttons = document.getElementsByTagName('alternativ')
  for (let b of buttons) {
    b.classList.remove('spelarval')
    b.classList.remove('datorval')
  }
  resultat.value = 'Lets Begin!'
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
    <KnappRad :knappar="knappar" @valdaKnappar="hittaVinnare" />
    <ResultatRad :valda-knappar="resultat" @vinnare="raknaPoeng" />
    <PoangRad :vinnare="vinnare" />
    <div class="Score">
      <button id="nolla" @click="reset">Nollställ poängen</button>
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
