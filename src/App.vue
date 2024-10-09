<script setup>
import { ref } from 'vue'
import KnappRad from './components/KnappRad.vue'

const score = ref({ spelare: 0, dator: 0 })
const resultat = ref('Lets Begin!')
const knappar = ref(['Sten', 'Sax', 'Påse', 'Lizard', 'Spock'])

function hittaVinnare() {
  let buttons = document.getElementsByClassName('alternativ')
  for (let b of buttons) {
    if (b.classList.contains('spelarval')) {
      var spelarval = b.textContent
    }
    if (b.classList.contains('datorval')) {
      var datorval = b.textContent
    }
  }
  if (spelarval == datorval) {
    resultat.value = 'Oavgjort!'
  } else if (
    (spelarval == 'Sten' && datorval == 'Sax') ||
    (spelarval == 'Sax' && datorval == 'Påse') ||
    (spelarval == 'Påse' && datorval == 'Sten')
  ) {
    resultat.value = 'Du vann!'
    score.value.spelare++
  } else {
    resultat.value = 'Du förlorade!'
    score.value.dator++
  }
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
</script>

<template>
  <header>
    <h1>Sten, Sax, Påse!</h1>
  </header>

  <main>
    <KnappRad :knappar="knappar" @valdaKnappar="hittaVinnare" />
    <div class="resultat">
      <p id="resultat">{{ resultat }}</p>
    </div>
    <div class="Score">
      <button id="nolla" @click="reset">Nollställ poängen</button>
      <p>
        <span id="spelare">{{ score.spelare }}</span> -
        <span id="dator">{{ score.dator }}</span>
      </p>
    </div>
  </main>
</template>

<style scoped>
header {
  text-align: center;
  margin-bottom: 1.2em;
}

.resultat {
  font-size: 1.2em;
  text-align: center;
  margin: 1.2em 0;
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
</style>
