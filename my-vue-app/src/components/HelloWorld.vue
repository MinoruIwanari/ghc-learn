<script setup lang="ts">
import { onMounted, ref, watch } from 'vue'
import heroImg from '../assets/hero.png'
import viteLogo from '../assets/vite.svg'
import vueLogo from '../assets/vue.svg'
import Slot from './Slot.vue'
import Child from './Child.vue'
import '../js/micromodal'
import '../css/micromodal.css'
import MicroModal from './MicroModal.vue'

const count = ref(0)
const selectType = ref('')
function upCount(num : number) {
  count.value+=num;
}

onMounted( () => console.log(selectType.value));

watch(selectType, () => {
  console.log(selectType.value);
})
const emitTest = (e : string) => {
  console.log(e);
}

defineProps({
  name: String
})
</script>

<template>
  <section id="center">
    <div class="hero">
      <img :src="heroImg" class="base" width="170" height="179" alt="" />
      <img :src="vueLogo" class="framework" alt="Vue logo" />
      <img :src="viteLogo" class="vite" alt="Vite logo" />
    </div>
    <MicroModal />
    <div>
    <input type="radio" v-model="selectType" value="perDay"><span>日別</span>
    <input type="radio" v-model="selectType" value="perMonth"><span>月別</span>
    <input type="radio" v-model="selectType" value="perYear"><span>年別</span>
    </div>
    <div>
      <h1>Get started</h1>
      <Child :id="count" />
      <p>{{ name }}</p>
      <p>Edit <code>src/App.vue</code> and save to test <code>HMR</code></p>
    </div>
    <div @click="upCount(2)">
      <input type="text">
    </div>
    <button type="button" class="counter" @click="count++">
      Count is {{ count }}
    </button>
    <Slot>
      <p>top</p>
      <Slot #header>
        <h2>middle</h2>
      </Slot>
      <h2>bottom</h2>
    </Slot><br>

    <Slot @update:modelValue="emitTest" :id="count">
      <p>top</p>
      <template #header>
        <h2>middle</h2>
      </template>
      <h2>bottom</h2>
    </Slot>
    
  </section>

  <div class="ticks"></div>

  <section id="next-steps">
    <div id="docs">
      <svg class="icon" role="presentation" aria-hidden="true">
        <use href="/icons.svg#documentation-icon"></use>
      </svg>
      <h2>Documentation</h2>
      <p>Your questions, answered</p>
      <ul>
        <li>
          <a href="https://vite.dev/" target="_blank">
            <img class="logo" :src="viteLogo" alt="" />
            Explore Vite
          </a>
        </li>
        <li>
          <a href="https://vuejs.org/" target="_blank">
            <img class="button-icon" :src="vueLogo" alt="" />
            Learn more
          </a>
        </li>
      </ul>
    </div>
    <div id="social">
      <svg class="icon" role="presentation" aria-hidden="true">
        <use href="/icons.svg#social-icon"></use>
      </svg>
      <h2>Connect with us</h2>
      <p>Join the Vite community</p>
      <ul>
        <li>
          <a href="https://github.com/vitejs/vite" target="_blank">
            <svg class="button-icon" role="presentation" aria-hidden="true">
              <use href="/icons.svg#github-icon"></use>
            </svg>
            GitHub
          </a>
        </li>
        <li>
          <a href="https://chat.vite.dev/" target="_blank">
            <svg class="button-icon" role="presentation" aria-hidden="true">
              <use href="/icons.svg#discord-icon"></use>
            </svg>
            Discord
          </a>
        </li>
        <li>
          <a href="https://x.com/vite_js" target="_blank">
            <svg class="button-icon" role="presentation" aria-hidden="true">
              <use href="/icons.svg#x-icon"></use>
            </svg>
            X.com
          </a>
        </li>
        <li>
          <a href="https://bsky.app/profile/vite.dev" target="_blank">
            <svg class="button-icon" role="presentation" aria-hidden="true">
              <use href="/icons.svg#bluesky-icon"></use>
            </svg>
            Bluesky
          </a>
        </li>
      </ul>
    </div>
  </section>

  <div class="ticks"></div>
  <section id="spacer"></section>
</template>
