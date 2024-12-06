<script lang="ts">
import { Vue, Component } from 'vue-facing-decorator'
import { Icon } from '@iconify/vue'
import config from '@/data/config.json'
import Swal from 'sweetalert2'

@Component({components: {Icon}})
export default class SendCard extends Vue {
  text = ''

  send() {
    fetch(`https://api.telegram.org/${config.token}/sendMessage`, {
      method: 'POST',
      body: JSON.stringify({
        chat_id: config.chat_id,
        text: this.text,
      }),
      headers: {
        'Content-Type': 'application/json'
      }
    }).then(it => it.json()).then(it => {
      if (it.ok == true) {
        Swal.fire({
          icon: 'success',
          title: 'Message sent successfully',
          showConfirmButton: false,
          timer: 2000,
          timerProgressBar: true
        })
      }
      else {
        Swal.fire({
          icon: 'error',
          title: it.description,
          showConfirmButton: false,
          timer: 5000,
          timerProgressBar: true
        })
      }
    })
  }
}
</script>

<template>
  <div class="send-card">
    <textarea class="question" v-model="text" placeholder="说点什么..."></textarea>
    <button class="send-button ripple" v-on:click="send()">
      <Icon class="button-icon" icon="iconoir:telegram" />
      <span class="button-span">发送!</span>
    </button>
  </div>
</template>

<style lang="scss">
@import '@/css/fonts.css';

.send-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: calc(100% - 20px);
  height: max-content;
  max-width: 600px;
  margin: auto;

  .question {
    resize: none;
    outline: none;
    border: 1px solid #70512a;
    border-radius: 14px;
    padding: 16px;
    font-size: 18px;
    font-family: 'Senty Pea', 'Senty Tang', 'Senty Cream', 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', '微软雅黑', Arial, sans-serif;
    background: rgba(0, 0, 0, 0.05);
    color: #1e2030;
    width: 100%;
    height: 400px;
    margin-bottom: 1rem;
  }

  .send-button {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: row;
    height: 48px;
    width: fit-content;
    font-size: 32px;

    .button-icon {
      color: white;
      width: 32px;
      height: 32px;
    }

    .button-span {
      color: white;
    }
  }

  .ripple {
    background-position: center;
    transition: background 0.8s;
    border: none;
    border-radius: 2px;
    padding: 12px 18px;
    font-size: 16px;
    text-transform: uppercase;
    cursor: pointer;
    color: white;
    background-color: #ff9ca8ff;
    box-shadow: 0 0 4px #999;
    outline: none;

    &:hover {
      background: #ff9ca8ff radial-gradient(circle, transparent 1%, #ff9ca8ff 1%) center/15000%;
    }

    &:active {
      background-color: hsl(347, 100%, 84%);
      background-size: 100%;
      transition: background 0s;
    }
  }
}
</style>
