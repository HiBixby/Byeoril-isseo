<template>
  <div class="description">Ctrl+Q를 눌러보세요!</div>
  <transition name="fade">
    <div v-if="isPressed" class="container">
      <transition name="fade">
        <PreviewMessage
          v-if="hover && !replyMsg"
          msg="혹시 궁금한거 있어?"
          hover="hover"
          @ReplyFromChild="OnReceivePreviewReply"
        />
      </transition>
      <div
        @mouseover="
          hover = true;
          newNoti = false;
        "
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
export default {
  name: "App",
  components: { PreviewMessage },
  data() {
    return {
      newNoti: true,
      hover: false,
      replyMsg: null,
      isPressed: false,
    };
  },
  methods: {
    OnReceivePreviewReply(message) {
      this.hover = false;
      this.replyMsg = message;
    },
  },
  mounted() {
    window.addEventListener("keydown", (event) => {
      if (event.key === "q" && event.ctrlKey === true) {
        console.log("단축키 눌림", event.key, event.ctrlKey);
        this.isPressed = true;
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
