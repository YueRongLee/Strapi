<template>
  <div id="app">
    <div id="app-toolbar">
      <div class="app-toolbar-left">
        <img
          class="app-toolbar-img"
          src="./assets/soldier1.jpeg"
          alt="logo"
          height="60px"
        />
        <span style="margin-left: 8px">不要看走開</span>
      </div>
      <div class="app-toolbar-right">
        <input
          class="app-toolbar-input"
          type="text"
          placeholder="輸入關鍵字搜尋"
        />
        <a class="app-toolbar-text" href="#">登入</a>
      </div>
      <!-- <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> -->
    </div>
    <div id="app-content">
      <div id="app-content-sidebar">
        <p class="app-content-sidebar-title">導覽列</p>
        <ul class="app-content-sidebar-list">
          <li
            class="app-content-li"
            v-for="nav in navs"
            :key="nav.name"
            @click="goto(nav.path)"
          >
            {{ nav.name }}
          </li>
        </ul>
      </div>
      <div id="app-content-body">
        <router-view />
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      navs: [
        {
          path: "/",
          name: "首頁",
        },
        {
          path: "/about",
          name: "介紹",
        },
        {
          path: "/draw-lots",
          name: "抽抽樂",
        },
      ],
    }
  },
  methods: {
    goto(path) {
      path === this.$route.path ? "" : this.$router.push(path)
    },
  },
}
</script>

<style>
html {
  height: 100%;
  display: flex;
}
body {
  margin: 0;
  width: 100%;
}
#app {
  display: flex;
  height: 100%;
  flex-direction: column;
  text-align: center;
  color: #2c3e50;
}

#app-toolbar {
  height: 60px;
  display: flex;
  justify-content: center;
  align-items: center;
  background: linear-gradient(rgb(215, 241, 255), rgb(198, 239, 255));
  box-shadow: 3px 3px 8px 0 #959595;
  z-index: 1;
  display: flex;
  justify-content: space-between;
}
.app-toolbar-left {
  display: flex;
  align-items: center;
}
.app-toolbar-img {
  border-radius: 30px;
}
.app-toolbar-right {
  margin-right: 20px;
}
.app-toolbar-input {
  border-radius: 10px;
  height: 30px;
  width: 200px;
  margin: 40px;
}
.app-toolbar-text {
  text-decoration: none;
  color: #4442b9;
}
.app-toolbar-text:hover {
  color: #a8a7ff;
}

#app-toolbar a.router-link-exact-active {
  color: #42b983;
}
#app-content {
  flex: 1;
  display: flex;
  background: linear-gradient(rgb(204, 255, 220), rgb(174, 227, 255));
  overflow: hidden;
}
#app-content-sidebar {
  width: 15%;
  background: linear-gradient(rgb(255, 232, 206), rgb(238, 255, 181));
  box-shadow: 3px 3px 8px 0 #959595;
  /* border-radius: 20px; */
  display: flex;
  flex-direction: column;
}
.app-content-sidebar-title {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 60px;
  margin: 0 0 12px 0;
  font-weight: bold;
  font-size: 20px;
  background: rgb(231, 231, 231);
  /* border-radius: 20px 20px 0 0; */
  box-shadow: 3px 3px 8px 0 #959595;
}
.app-content-sidebar-list {
  user-select: none;
  width: 100%;
  font-size: 16px;
  margin: 0;
}
#app-content-sidebar ul {
  padding-inline-start: 0;
}
#app-content-body {
  flex: 1;
  padding: 20px;
  border-radius: 20px;
  overflow: scroll;
}
.app-content-li {
  margin: 0 10px;
  height: 50px;
  cursor: pointer;
  list-style: none;
  color: rgb(51, 139, 255);
  display: flex;
  align-items: center;
  justify-content: center;
  border-bottom: 1px solid rgb(192, 192, 192);
  background: rgb(228, 240, 255);
}
.app-content-li:hover {
  background: rgb(193, 215, 255);
  box-shadow: 2px 2px 10px 2px #8fa7a2;
  transform: translateY(2px);
  transition: all 0.1s ease-out;
}
</style>
