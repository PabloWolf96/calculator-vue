<template>
  <div class="container">
    <screen :input="input" :calc="calc" :limit="limit" />
    <app-body
      @numClicked="handleNumClick"
      @clear="handleClear"
      @multiply="multiply"
      @add="add"
      @minus="minus"
      @solve="solve"
      @periodClicked="periodClicked"
      :limit="limit"
    />
  </div>
</template>

<script>
import Screen from "./components/Screen.vue";
import AppBody from "./components/Body.vue";
export default {
  components: { AppBody, Screen },
  data() {
    return {
      input: "0",
      calc: "",
    };
  },
  methods: {
    handleNumClick(val) {
      if (this.limit) {
        return;
      }
      if (this.input === "0") {
        this.input = val;
        this.calc = val;
      } else {
        this.calc = this.calc.split("=")[0] + val;
        this.input = this.input.split(/[+\-/*]/)[0] + val;
      }
    },
    handleClear() {
      this.input = "0";
      this.calc = "";
    },
    multiply(val) {
      let regEx = /\d/;
      this.input = val;
      if (regEx.test(this.lastChar)) {
        this.calc = this.calc.split("=")[0] + val;
      } else if (regEx.test(this.secondToLastChar)) {
        this.calc = this.calc.slice(0, this.calc.length - 1) + val;
      } else {
        this.calc = this.calc.slice(0, this.calc.length - 2) + val;
      }
    },
    add(val) {
      let regEx = /\d/;
      this.input = val;
      if (regEx.test(this.lastChar)) {
        this.calc = this.calc.split("=")[0] + val;
      } else if (this.lastChar === "-") {
        if (regEx.test(this.secondToLastChar)) {
          this.calc = this.calc.split("=")[0] + val;
        } else {
          this.calc = this.calc.slice(0, this.calc.length - 2) + val;
        }
      } else {
        this.calc = this.calc.slice(0, this.calc.length - 1) + val;
      }
    },
    minus(val) {
      let regEx = /\d/;
      this.input = val;
      if (regEx.test(this.lastChar) || regEx.test(this.secondToLastChar)) {
        this.calc = this.calc.split("=")[0] + val;
      } else if (val !== "-") {
        this.calc = this.calc.slice(0, this.calc.length - 2) + val;
      }
    },
    solve() {
      let answer = eval(this.calc);
      this.calc += "=" + answer;
      this.input = answer;
    },
    periodClicked(val) {
      let regEx = /\d/;
      if (this.limit) {
        return;
      }
      if (this.calc === "") {
        this.calc = "0.";
        this.input += val;
      } else if (regEx.test(this.lastChar)) {
        this.calc = this.calc.split("=")[0] + val;
        this.input += ".";
      }
    },
  },
  computed: {
    limit() {
      return this.input.length > 18;
    },
    lastChar() {
      return this.calc[this.calc.length - 1];
    },
    secondToLastChar() {
      return this.calc[this.calc.length - 2];
    },
  },
};
</script>

<style></style>
