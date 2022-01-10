<template>
  <div class="container-body">
    <app-button
      v-for="button in buttons"
      :key="button.content"
      :btn="button.content"
      :styles="button.styles"
      @clicked="handleClick"
      :data-type="button.type"
    />
  </div>
</template>

<script>
import AppButton from "./Button.vue";
export default {
  components: { AppButton },
  props: ["limit"],
  data() {
    return {
      buttons: [
        {
          type: "fn",
          content: "AC",
          styles: "background-color: #ac3939; color:white; grid-column: span 2",
        },
        {
          type: "fn",
          content: "/",
          styles: "background-color: #666; color: white",
        },
        {
          type: "fn",
          content: "*",
          styles: "background-color: #666; color: white",
        },
        {
          type: "number",
          content: "7",
          styles: "background-color: #4d4d4d; color:white",
        },
        {
          type: "number",
          content: "8",
          styles: "background-color: #4d4d4d; color:white",
        },
        {
          type: "number",
          content: "9",
          styles: "background-color: #4d4d4d; color:white",
        },
        {
          type: "fn",
          content: "-",
          styles: "background-color: #666; color: white",
        },
        {
          type: "number",
          content: "4",
          styles: "background-color: #4d4d4d; color:white",
        },
        {
          type: "number",
          content: "5",
          styles: "background-color: #4d4d4d; color:white",
        },
        {
          type: "number",
          content: "6",
          styles: "background-color: #4d4d4d; color:white",
        },
        {
          type: "fn",
          content: "+",
          styles: "background-color: #666; color: white",
        },
        {
          type: "number",
          content: "1",
          styles: "background-color: #4d4d4d; color:white",
        },
        {
          type: "number",
          content: "2",
          styles: "background-color: #4d4d4d; color:white",
        },
        {
          type: "number",
          content: "3",
          styles: "background-color: #4d4d4d; color:white",
        },
        {
          type: "fn",
          content: "=",
          styles: "background-color: #004466; color: white; grid-row: span 2",
        },
        {
          type: "number",
          content: "0",
          styles: "background-color: #4d4d4d; color:white; grid-column: span 2",
        },
        {
          type: "fn",
          content: ".",
          styles: "background-color: #4d4d4d; color:white",
        },
      ],
    };
  },
  methods: {
    handleClick(val) {
      let btnClickedValue = val;

      let numericRegEx = /\d/;

      if (numericRegEx.test(btnClickedValue)) {
        this.$emit("numClicked", btnClickedValue);
      } else if (btnClickedValue === "AC") {
        this.$emit("clear");
      } else if (val === "*" || val === "/") {
        this.$emit("multiply", val);
      } else if (val === "+") {
        this.$emit("add", val);
      } else if (val === "-") {
        this.$emit("minus", val);
      } else if (val === "=") {
        this.$emit("solve");
      } else if (val === ".") {
        this.$emit("periodClicked", val);
      }
    },
  },
};
</script>

<style></style>
