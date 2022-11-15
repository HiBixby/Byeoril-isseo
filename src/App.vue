<template>
  <div class="box">
    <div class="ping"></div>
    <div class="new">
    </div>
    <img class="avata" src="./assets/avata.svg" alt="별이" />
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
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
.box {
  background-color: white;
  width: 4.5rem;
  height: 4.5rem;
  display: flex;
  border-radius: 25px;
  justify-content: center;
  align-items: center;
  position: fixed;
  bottom: 3rem;
  right: 3rem;
  box-shadow:  0 0 1px rgb(0 0 0 / 10%), 0 2px 5px rgb(0 0 0 / 10%)
}
.box:hover{
  cursor: pointer;
}
.new {
  background-image:url('./assets/bang.svg');
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
  color:white;
}
.ping{
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
  color:white;
  opacity: 75%;
	animation: ping 2s cubic-bezier(0, 0, 0.2, 1) infinite;

}
.avata {
  padding: 1rem;
}

@keyframes ping {
  75%, 100% {
    transform: scale(1.5);
    opacity: 0;
  }
}
</style>
