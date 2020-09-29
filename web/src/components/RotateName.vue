<template>
  <div>
    <div class="my-wrapper">
      <div v-for="n in 10" :key="n" class="my-light" />
      <div class="my-panel">
        <div class="my-sector" v-for="(award, index) in awards" :key="index">
          <div class="my-sector-inner">
            <span>{{ award }}</span>
          </div>
        </div>
        <div class="my-name-pointer" @click="start">开始抽奖</div>
      </div>
    </div>
    <div class="my-name-result"></div>
    <div></div>
  </div>
</template>
<script>
export default {
  props: ["awards"],
  data() {
    return {
      isRotate: false,
      reward: [],
      myResults: [],
      myRewardText: "",
    }
  },
  methods: {
    start() {
      // console.log("開始抽獎")
    },
  },
  watch: {
    awards: {
      handler(data) {
        console.log(data)
        this.reward = data
      },
    },
    myRewardText: {
      handler(data) {
        this.myResults.push({ name: data })

        const counts = {}
        this.myResults.forEach((r) => {
          counts[r.name] = counts[r.name] ? counts[r.name] + 1 : 1
        })
        console.log(counts)
      },
    },
  },
  mounted() {
    let getEle = document.getElementsByClassName.bind(document)
    let pointer = getEle("my-name-pointer")[0]
    let result = getEle("my-name-result")[0]
    let lights = Array.prototype.slice.call(getEle("my-light"))

    let onRotation = false // 记录当前是否正在旋转，如果正在旋转，就不能继续点击了
    this.reward = this.awards

    // 根据随机角度获取奖励
    const that = this
    let getReward = (function() {
      let currentDeg = 0
      return function() {
        // 转三圈到四圈
        let rotateDeg = Math.random() * 360 + 5040
        currentDeg += rotateDeg
        let rewardText = that.reward[Math.floor(((currentDeg + 15) % 360) / 36)]

        that.myRewardText = rewardText

        return {
          deg: currentDeg,
          text:
            rewardText === "銘謝惠顧"
              ? "你沒有獲得獎品。"
              : "恭喜: " + rewardText,
        }
      }
    })()

    pointer.addEventListener("click", () => {
      if (onRotation) return
      // console.log("開始抽獎")
      onRotation = true
      lights.forEach((light) => {
        light.className += " my-light-twinkling"
      })
      let nextStatus = getReward()
      // console.log(nextStatus)
      result.innerText = nextStatus.text

      result.style.display = "none"
      pointer.style.transform = `rotateZ(${nextStatus.deg}deg)`
    })
    pointer.addEventListener("transitionend", () => {
      // console.log("抽獎結束")
      setTimeout(() => {
        onRotation = false
        lights.forEach((light) => {
          light.className = "my-light"
        })
        result.style.display = "block"
      }, 300)
    })
  },
}
</script>

<style scoped>
.my-wrapper {
  position: relative;
  height: 200px;
  width: 200px;
  padding: 20px;
  margin: 20px 60px;
  background-color: #ff5555;
  box-shadow: #000000 0px 0px 10px;
  border-radius: 50%;
}
.my-light {
  position: absolute;
  height: 10px;
  width: 10px;
  border-radius: 50%;
  top: 5px;
  left: 115px;
  transform-origin: 5px 115px;
}
.my-light-twinkling {
  animation: 1s twinkling 3, 100ms 3s twinkling 3;
}
.my-light:nth-child(2n) {
  background-color: #fafce7;
}
.my-light:nth-child(2n + 1) {
  background-color: #ffe58b;
}
.my-light:nth-child(2) {
  transform: rotate(36deg);
}
.my-light:nth-child(3) {
  transform: rotate(72deg);
}
.my-light:nth-child(4) {
  transform: rotate(108deg);
}
.my-light:nth-child(5) {
  transform: rotate(144deg);
}
.my-light:nth-child(6) {
  transform: rotate(180deg);
}
.my-light:nth-child(7) {
  transform: rotate(216deg);
}
.my-light:nth-child(8) {
  transform: rotate(252deg);
}
.my-light:nth-child(9) {
  transform: rotate(288deg);
}
.my-light:nth-child(10) {
  transform: rotate(324deg);
}
.my-panel {
  position: relative;
  height: 200px;
  width: 200px;
  background-color: #b7b7b7;
  border-radius: 100px;
}
.my-sector {
  position: absolute;
  left: 100px;
  top: 0px;
  width: 100px;
  height: 200px;
  font-size: 14px;
  border-radius: 0px 100px 100px 0;
  overflow: hidden;
  transform-origin: left center;
}
.my-sector:nth-child(1) {
  transform: rotate(-18deg);
}
.my-sector:nth-child(2) {
  transform: rotate(18deg);
}
.my-sector:nth-child(3) {
  transform: rotate(54deg);
}
.my-sector:nth-child(4) {
  transform: rotate(90deg);
}
.my-sector:nth-child(5) {
  transform: rotate(126deg);
}
.my-sector:nth-child(6) {
  transform: rotate(162deg);
}
.my-sector:nth-child(7) {
  transform: rotate(198deg);
}
.my-sector:nth-child(8) {
  transform: rotate(234deg);
}
.my-sector:nth-child(9) {
  transform: rotate(270deg);
}
.my-sector:nth-child(10) {
  transform: rotate(306deg);
}
.my-sector:nth-child(2n + 1) .my-sector-inner {
  background: #fef6e0;
}
.my-sector:nth-child(2n) .my-sector-inner {
  background: #ffffff;
}
.my-sector-inner {
  text-align: center;
  display: block;
  width: 40px;
  padding: 5px 3px 0 57px;
  height: 195px;
  transform: translateX(-100px) rotate(36deg);
  transform-origin: right center;
  border-radius: 100px 0 0 100px;
}
.my-sector-inner span {
  display: block;
  transform-origin: center;
  transform: rotate(-10deg);
  padding-left: 10px;
  color: #d46854;
}
.my-name-pointer {
  cursor: pointer;
  position: absolute;
  left: 79px;
  top: 79px;
  z-index: 10;
  height: 30px;
  width: 30px;
  padding: 6px;
  color: #fff899;
  line-height: 15px;
  font-size: 12px;
  text-align: center;
  background-color: #ff5350;
  border-radius: 50%;
  border: 1px solid #ff5350;
  transition: transform 3s cubic-bezier(0.2, 0.93, 0.43, 1);
}
.my-name-pointer::after {
  content: "";
  position: absolute;
  left: 14px;
  top: -24px;
  border-width: 12px 6px;
  border-style: solid;
  border-color: transparent;
  border-bottom-color: #ff5350;
  transform-origin: center;
}
.my-name-result {
  margin: 20px 10px;
}

@keyframes twinkling {
  50% {
    background: transparent;
  }
}
</style>
