<template>
  <div class="chating-room">
    <div class="nav">
      <button @click="CloseChatingRoom" class="btn-back">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="8.027"
          height="14.53"
          viewBox="0 0 8.027 14.53"
        >
          <path
            id="뒤로가기_버튼"
            data-name="뒤로가기 버튼"
            d="M27.174,23.565,20.98,29.759,27.2,35.974"
            transform="translate(-20.23 -22.504)"
            fill="none"
            stroke="#606061"
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="1.5"
          />
        </svg>
      </button>
      <span class="nav-name"> 별이 </span>
      <button class="btn-detail">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="4"
          height="16.366"
          viewBox="0 0 4 16.366"
        >
          <g
            id="더보기_버튼"
            data-name="더보기 버튼"
            transform="translate(-1776.503 -614.139)"
          >
            <path
              id="패스_96"
              data-name="패스 96"
              d="M528.5,30.322a2,2,0,1,1-2-2,2,2,0,0,1,2,2"
              transform="translate(1252 592)"
              fill="#606061"
            />
            <path
              id="패스_97"
              data-name="패스 97"
              d="M528.5,24.139a2,2,0,1,1-2-2,2,2,0,0,1,2,2"
              transform="translate(1252 592)"
              fill="#606061"
            />
            <path
              id="패스_98"
              data-name="패스 98"
              d="M528.5,36.505a2,2,0,1,1-2-2,2,2,0,0,1,2,2"
              transform="translate(1252 592)"
              fill="#606061"
            />
          </g>
        </svg>
      </button>
      <button @click="CloseChatingRoom" class="btn-close">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="13.267"
          height="13.266"
          viewBox="0 0 13.267 13.266"
        >
          <g
            id="닫기_버튼"
            data-name="닫기 버튼"
            transform="translate(-1825.309 -545.19)"
          >
            <line
              id="선_1"
              data-name="선 1"
              y1="11.37"
              x2="11.37"
              transform="translate(1826.258 546.138)"
              fill="none"
              stroke="#606061"
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="1.341"
            />
            <line
              id="선_2"
              data-name="선 2"
              x1="11.37"
              y1="11.37"
              transform="translate(1826.257 546.138)"
              fill="none"
              stroke="#606061"
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="1.341"
            />
          </g>
        </svg>
      </button>
    </div>
    <div class="conversation-container">
      <div class="time">
        {{ getHoursAndMinutes(conversation[0].time) }}
      </div>
      <div v-for="(message, index) in conversation" :key="index">
        <div v-if="isByeoli(message)" class="sender-name">별이</div>
        <div
          class="message-line"
          :class="{ byeoli: isByeoli(message), me: isMe(message) }"
        >
          <div v-if="isByeoli(message)" class="avata">
            <img src="../assets/avata.svg" />
          </div>
          <div
            class="bubble"
            :class="{ byeoli: isByeoli(message), me: isMe(message) }"
          >
            <div>{{ message.msg }}</div>
          </div>
        </div>
      </div>
    </div>
    <div class="send-container">
      <form @submit.prevent="onSubmitReply">
        <textarea
          @keydown.enter.exact.prevent="onSubmitReply"
          v-model="replyMsg"
          row="3"
          spellcheck="false"
          autofocus
        ></textarea>
        <button type="submit" class="btn-send" v-bind:disabled="!replyMsg">
          전송
        </button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "ChatingRoom",
  props: {
    conversation: Array,
  },
  data() {
    return {
      close: false,
      replyMsg: null,
    };
  },
  methods: {
    isByeoli(message) {
      return message.sender === "byeoli" ? true : false;
    },
    isMe(message) {
      return message.sender === "me" ? true : false;
    },
    getHoursAndMinutes(time) {
      return time.toLocaleTimeString("en-US", {
        hour: "2-digit",
        minute: "2-digit",
      });
    },
    onSubmitReply() {
      if (this.replyMsg) {
        this.$emit("ReplyFromChild", this.replyMsg);
        this.replyMsg = null;
      }
    },
    CloseChatingRoom() {
      this.$emit("CloseChatingRoom");
    },
  },
  computed: {},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.chating-room {
  position: relative;
  bottom: 0.996rem;
  width: 23.151rem;
  min-height: 27.054rem;
  max-height: 45rem;
  border-radius: 32px;
  background-color: white;
  box-shadow: 0 0 1px rgb(0 0 0 / 10%), 0 2px 5px rgb(0 0 0 / 10%);
  overflow: hidden;
  display: flex;
  flex-direction: column;
  transition-delay: height 1s ease;
}
.nav {
  min-height: 3.687rem;
  background-color: #f1f1f2;
  display: flex;
  align-items: center;
  justify-content: center;
}
.nav button {
  border: 0;
  outline: none;
  padding: 0;
  display: flex;
  align-items: center;
}
button {
  cursor: pointer;
}
button:disabled {
  cursor: default;
}
.nav-name {
  margin: 0 58.5% 0 8.8%;
  font-size: 0.918rem;
  font-weight: 600;
}
.btn-detail {
  margin-right: 7.5%;
}
.conversation-container {
  flex: 1;
  display: flex;
  flex-direction: column;
  overflow: scroll;
}
.time {
  margin: 0.828rem 0 0 0;
}
.send-container {
  height: 6.144rem;
  background-color: #f1f1f2;
}
.send-container form {
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-end;
}
.send-container textarea {
  display: block;
  width: 100%;
  height: 3.607rem;
  border: 0;
  outline: none;
  background: transparent;
  font-family: inherit;
  box-sizing: border-box;
  font-size: 0.917rem;
  font-weight: 600;
  color: inherit;
  padding: 0.833rem 3.6%;
  resize: none;
}
.btn-send {
  box-sizing: border-box;
  display: block;
  border: none;
  outline: none;
  background-color: #ffe795;
  border-radius: 14.332px;
  width: 16.1%;
  font-size: 0.918rem;
  font-weight: 600;
  font-family: inherit;
  margin: 0 0.806rem 0.746rem 0;
  padding: 0.355rem 0 0.374rem 0;
}
.sender-name {
  text-align: left;
  font-size: 0.554rem;
  font-weight: 600;
  color: #999999;
  margin-left: 13.5%;
  margin-bottom: 0.428rem;
}
.message-line {
  display: flex;
  align-items: center;
  margin-bottom: 0.7rem;
}
.me.message-line {
  justify-content: right;
}
.avata {
  background-color: #f1f1f2;
  width: 6.6%;
  height: 6.6%;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0;
  border-radius: 10px;
  margin-left: 2.5%;
  margin-right: 1.1%;
}
.avata img {
  width: 0.967rem;
  height: 0.926rem;
  padding: 0.318rem 0.258rem 0.289rem 0.308rem;
}
.bubble {
  box-sizing: border-box;
  border-radius: 18px;
  width: auto;
  max-width: 70%;
  text-align: left;
}
.byeoli.bubble {
  background-color: #f1f1f2;
}
.bubble div {
  box-sizing: border-box;
  width: 100%;
  height: 100%;
  padding: 0.5rem 0.9rem;
  font-size: 0.917rem;
  font-weight: 600;
  white-space: break-spaces;
  overflow-wrap: break-word;
}
.me.bubble {
  background-color: #ffe795;
  margin-right: 3.1%;
}
</style>
