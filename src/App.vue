<script lang="ts">
import { Vue, Component } from 'vue-facing-decorator';
import SendCard from '@/components/SendCard.vue'
import topHtml from '@/assets/top.md'
import bottomHtml from '@/assets/bottom.md'

@Component({components: {SendCard}})
export default class App extends Vue {
  topHtml = topHtml;
  bottomHtml = bottomHtml;
}
</script>

<template>
  <div class="markdown" v-html="topHtml" ></div>
  <SendCard/>
  <div class="markdown" v-html="bottomHtml" ></div>
</template>

<style lang="scss">
@import '@/css/markdown.scss';

body {
  background-color: #ffeedb;
}

#app {
  width: 100%;
  height: 100%;
  min-height: 100vh;
  max-width: 900px;
  margin: auto;
}
</style>
