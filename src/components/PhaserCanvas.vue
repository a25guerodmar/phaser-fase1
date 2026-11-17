<script setup>
import { ref, watch, onMounted, onUnmounted } from 'vue';
import Phaser from 'phaser';
import { MainScene } from '../game/MainScene';

const props = defineProps([
  'nomUsuari',
  'colorAvatar',
  'estat'
]);

const contenidor = ref(null);
let game = null;

onMounted(() => {

  game = new Phaser.Game({
    type: Phaser.AUTO,
    width: 640,
    height: 400,
    backgroundColor: '#1e293b',
    parent: contenidor.value,
    scene: [MainScene]
  });

  game.events.once('ready', () => {
    const escena = game?.scene.getScene('MainScene');

    escena?.actualitzarNom(props.nomUsuari);
    escena?.canviarColor(props.colorAvatar);
    escena?.actualitzarEstat(props.estat);
  });

});

watch(() => props.nomUsuari, (nouNom) => {
  const escena = game?.scene.getScene('MainScene');
  escena?.actualitzarNom(nouNom);
});

watch(() => props.colorAvatar, (nouColor) => {
  const escena = game?.scene.getScene('MainScene');
  escena?.canviarColor(nouColor);
});

watch(() => props.estat, (nouEstat) => {
  const escena = game?.scene.getScene('MainScene');
  escena?.actualitzarEstat(nouEstat);
});

function canviarPausa(pausar) {
  const escena = game?.scene.getScene('MainScene');

  if (pausar) {
    escena?.scene.pause();
  } else {
    escena?.scene.resume();
  }
}

defineExpose({
  canviarPausa
});

onUnmounted(() => {
  game?.destroy(true);
});

</script>

<template>
  <div ref="contenidor"></div>
</template>