<template>
  <div id="app">
    <h2>CSS3 Perspective Playground</h2>
    <main>
      <section class="settings">
        <div class="settings-container">
          <label>perspective: {{ perspective }}px;</label>
          <input v-model="perspective" type="range" min="0" max="999" />

          <label>{{ rotateX }}: 0deg; </label>
          <input v-model="rotateX" type="range" min="-180" max="180" />

          <label>{{ rotateY }}: 0deg; </label>
          <input v-model="rotateY" type="range" min="-180" max="180" />

          <label>{{ rotateZ }}: 0deg; </label>
          <input v-model="rotateZ" type="range" min="-180" max="180" />

          <button @click="reset" type="button">Reset</button>
          <button @click="copy" type="button">Copy</button>
        </div>
      </section>
      <section class="output">
        <div ref="box" class="box-container">
          <div :style="setPerspective" class="box"></div>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      perspective: 0,
      rotateX: 0,
      rotateY: 0,
      rotateZ: 0,
      text: "",
    };
  },
  computed: {
    setPerspective() {
      return {
        transform: `
        perspective(${this.perspective}px)
        rotateX(${this.rotateX}deg)
        rotateY(${this.rotateY}deg)
        rotateZ(${this.rotateZ}deg)
      `,
      };
    },
    setRotateX() {
      return `${this.rotateX}px`;
    },
  },

  methods: {
    reset() {
      this.perspective = 0;
      this.rotateX = 0;
      this.rotateY = 0;
      this.rotateZ = 0;
    },
    copy() {
      const el = document.createElement("textarea");
      el.value = `transform : ${this.setPerspective.transform}`;
      el.setAttribute("readonly", "");
      el.style.position = "absolute";
      el.style.left = "-9999px";
      const data = this.$refs.box.appendChild(el);
      data.select();
      document.execCommand("copy");
      this.$refs.box.removeChild(el);
    },
  },
};
</script>

<style>
html {
  box-sizing: border-box;
  width: 100%;
  height: 100%;
}

*,
*:before,
*:after {
  box-sizing: inherit;
  padding: 0;
  margin: 0;
}
body {
  font-family: sans-serif;
  height: 100%;
  margin: 0;
  background: #261c33;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
}

h2 {
  color: #8d81f3;
  text-align: center;
  font-size: 40px;
  margin: 20px;
}
main {
  display: flex;
  justify-content: space-around;
  align-items: center;
  height: 420px;
  max-width: 768px;
  margin: 0 auto;
  font-family: monospace, sans-serif;
  font-size: 22px;
}
main label {
  display: block;
}
main input[type="range"] {
  display: block;
  margin-bottom: 10px;
  width: 200px;
}
section.settings {
  width: 50%;
  z-index: 2;
}
.box-container {
  padding: 50px;
  border: 1px solid #8d81f3;
}
.box {
  width: 150px;
  height: 150px;
  background: #8d81f3;
}

button {
  background-color: #8d81f3;
  color: #fff;
  display: inline-block;
  font-size: 20px;
  padding: 10px;
  outline: none;
  border: none;
  margin-right: 10px;
}

label {
  color: #fff;
}
</style>
