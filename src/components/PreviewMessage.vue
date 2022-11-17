<template>
  <div class="preview">
    <div class="sender-info">
      <div class="avata-preview">
        <img class="avata-preview-img" src="../assets/avata.svg" />
      </div>
      <span class="name">별이</span>
      <span class="time">{{ getHoursAndMinutes }}</span>
    </div>
    <div class="message-content">{{ msg }}</div>
    <form @submit.prevent="onSubmitReply">
      <input class="reply" v-model="replyMsg" />
    </form>
  </div>
</template>

<script>
export default {
  name: "PreviewMessage",
  props: {
    sender: String,
    msg: String,
    isPreview: Boolean,
    time: null,
  },
  data() {
    return {
      replyMsg: null,
    };
  },
  methods: {
    onSubmitReply() {
      console.log(this.replyMsg);
      this.$emit("ReplyFromChild", this.replyMsg);
    },
  },
  computed: {
    getHoursAndMinutes() {
      return this.time.toLocaleTimeString("en-US", {
        hour: "2-digit",
        minute: "2-digit",
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
  padding: 0.515rem 0.82rem 0.442rem;
  color:inherit;
}
.reply {
  border: none;
  background-color: #ffe795;
  width: 93.7%;
  height: 2.62rem;
  border-radius: 11.5px;
  color: inherit;
  font-family: inherit;
  font-size: 1rem;
  font-weight: 600;
  padding: 0 0.897rem;
  box-sizing: border-box;
}
.reply:focus {
  outline: none;
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
</style>
