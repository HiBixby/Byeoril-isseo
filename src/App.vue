<template>
  <div class="description">
    Ctrl+Q를 눌러보세요!<br /><span style="color: skyblue">다크모드</span>라고
    입력해보세요!
  </div>
  <transition name="fade">
    <div v-if="isHotkeyPressed" class="container">
      <transition name="fade">
        <PreviewMessage
          v-if="isPreview"
          v-bind:msg="conversation[conversation.length - 1].msg"
          v-bind:time="conversation[conversation.length - 1].time"
          @ReplyFromChild="OnReceivePreviewReply"
        />
      </transition>
      <transition name="fade">
        <ChatingRoom
          v-if="isChatingRoom"
          v-bind:conversation="conversation"
          v-bind:isChatingRoom="isChatingRoom"
          @CloseChatingRoom="CloseChatingRoom"
          @ReplyFromChild="OnReceivePreviewReply"
        >
        </ChatingRoom>
      </transition>
      <div
        @mouseover="
          if (!replyMsg) {
            isPreview = true;
            newNoti = false;
          }
        "
        @click="OnClickBox()"
        class="box"
      >
        <div v-if="newNoti">
          <div class="ping"></div>
          <div class="new"></div>
        </div>
        <img class="avata" src="./assets/avata.svg" alt="별이" />
      </div>
    </div>
  </transition>
</template>

<script>
import PreviewMessage from "./components/PreviewMessage.vue";
import ChatingRoom from "./components/ChatingRoom.vue";
export default {
  name: "App",
  components: { PreviewMessage, ChatingRoom },
  data() {
    return {
      newNoti: true,
      isPreview: false,
      replyMsg: null,
      isHotkeyPressed: false,
      conversation: [],
      isChatingRoom: false,
      response: {
        "오늘 점심 메뉴 추천 좀": ["돈가스"],
        다크모드: [
          "아 다크모드! 우선 설정에 들어가봐~",
          "거기서 '모양'탭 → 다크모드ON 하면 돼!\n아니면 지금 내가 도와줄까?\n스위치 한번 눌러봐~",
        ],
      },
    };
  },
  methods: {
    OnReceivePreviewReply(message) {
      this.isPreview = false;
      this.replyMsg = message;
      this.isChatingRoom = true;
      this.OnReceiveReply(message);
    },
    OnReceiveReply(message) {
      this.conversation.push({
        sender: "me",
        msg: message,
        time: new Date(),
      });
      if (message in this.response) {
        for (let i in this.response[message]) {
          this.conversation.push({
            sender: "byeoli",
            msg: this.response[message][i],
            time: new Date(),
          });
        }
      } else {
        this.conversation.push({
          sender: "byeoli",
          msg: "무슨 말이야?",
          time: new Date(),
        });
      }
      console.log(this.conversation);
    },
    OnClickBox() {
      console.log("[Function] OnClickBox");
      console.log(this.isPreview);
      if (!this.isPreview) {
        this.OpenChatingRoom();
      }
    },
    OpenChatingRoom() {
      this.isChatingRoom = true;
    },
    CloseChatingRoom() {
      this.isChatingRoom = false;
    },
  },
  mounted() {
    window.addEventListener("keydown", (event) => {
      if (
        event.key === "q" &&
        event.ctrlKey === true &&
        !this.isHotkeyPressed
      ) {
        console.log("단축키 눌림", event.key, event.ctrlKey);
        this.isHotkeyPressed = true;
        this.conversation.push({
          sender: "byeoli",
          msg: "혹시 궁금한거 있어?",
          time: new Date(),
        });
      }
    });
  },
};
</script>

<style>
#app {
  font-family: "Pretendard Variable", Pretendard, -apple-system,
    BlinkMacSystemFont, system-ui, Roboto, "Helvetica Neue", "Segoe UI",
    "Apple SD Gothic Neo", "Noto Sans KR", "Malgun Gothic", "Apple Color Emoji",
    "Segoe UI Emoji", "Segoe UI Symbol", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%;
}
.description {
  font-size: xx-large;
  font-weight: 700;
}
.container {
  position: fixed;
  bottom: 3rem;
  right: 3rem;
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}
.sender-info {
  display: flex;
  align-items: center;
  padding: 0.621rem 0.644rem 0rem;
}
.avata-preview {
  width: 1.759rem;
  height: 1.759rem;
  background-color: #f2f1ed;
  border-radius: 11.5px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.avata-preview img {
  width: 1.109rem;
  height: 1.063rem;
}
.name {
  font-size: 0.711rem;
  font-weight: 600;
  padding: 0 0.452rem 0 0.746rem;
}
.time {
  color: #989898;
  font-size: 0.711rem;
  font-weight: 500;
}
.message-content {
  font-size: 0.918rem;
  font-weight: 600;
  text-align: left;
  line-height: 1.2;
  color: #000;
  padding: 0.515rem 0.82rem 0.442rem;
}
.reply {
  border: none;
  background-color: #ffe795;
  width: 93.7%;
  height: 2.62rem;
  border-radius: 11.5px;
  caret-color: black;
  font-size: 1.275rem;
  font-weight: 600;
  padding: 0 0.897rem;
  box-sizing: border-box;
}
.reply:focus {
  outline: none;
}
.box {
  background-color: white;
  width: 4.5rem;
  height: 4.5rem;
  display: flex;
  border-radius: 25px;
  justify-content: center;
  align-items: center;
  box-shadow: 0 0 1px rgb(0 0 0 / 10%), 0 2px 5px rgb(0 0 0 / 10%);
  position: relative;
  bottom: 0;
  right: 0;
}
.box:hover {
  cursor: pointer;
}
.new {
  background-image: url("./assets/bang.svg");
  background-size: 0.217rem 0.873rem;
  background-repeat: no-repeat;
  background-position: center;
  position: absolute;
  width: 1.835rem;
  height: 1.835rem;
  left: 2.926rem;
  bottom: 3.228rem;
  border-radius: 100%;
  background-color: #cc5458;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
}
.ping {
  position: absolute;
  width: 1.835rem;
  height: 1.835rem;
  left: 2.926rem;
  bottom: 3.228rem;
  border-radius: 100%;
  background-color: #cc5458;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  opacity: 75%;
  animation: ping 2s cubic-bezier(0, 0, 0.2, 1) infinite;
}
.avata {
  padding: 1rem;
}

@keyframes ping {
  75%,
  100% {
    transform: scale(1.5);
    opacity: 0;
  }
}
.preview {
  position: relative;
  bottom: 0.715rem;
  width: 23.12rem;
  height: 7.815rem;
  border-radius: 21px;
  background-color: white;
  box-shadow: 0 0 1px rgb(0 0 0 / 10%), 0 2px 5px rgb(0 0 0 / 10%);
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
