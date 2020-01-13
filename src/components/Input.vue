<template>
  <div class="input">
    <textarea id="codeInput" maxlength="500" v-model="inputParam"></textarea>
    <button @click="descInput">Run</button>
    <span id="notify">{{plotterParam}}</span>
  </div>
</template>

<script>
export default {
  name: "SvgInput",
  data() {
    return {
      inputParam: "",
      plotterParam: ""
    };
  },
  methods: {
    descInput() {
      if (this.inputParam) {
        let template = this.inputParam.split(/\r?\n/g);
        this.$emit("getAttributes", template);
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.input {
  display: flex;
  flex-direction: column;
}
textarea {
  box-sizing: border-box;
  border: none;
  border-radius: 0.5rem;
  resize: none;
  font-size: 1rem;
  line-height: 1.2;
  overflow: auto;
  padding: 0.5rem;
  box-shadow: 0 0.25rem 1rem -0.5rem black;
  width: 40vw;
  height: 30vh;
  background: #2f2e2e;
  color: palegreen;
}
button {
  font-family: inherit;
  font-size: inherit;
  color: inherit;
  background: none;
  cursor: pointer;
  padding: 25px 80px;
  display: inline-block;
  margin: 15px 30px;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: 700;
  outline: none;
  position: relative;
  -webkit-transition: all 0.3s;
  -moz-transition: all 0.3s;
  transition: all 0.3s;
  border: 3px solid #ccc;
}

button:hover{
  background: #0e83cd;
  color: white;
  padding-left: 60%;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
