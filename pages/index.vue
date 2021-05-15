<template>
  <div class="container">
    <input-property-area @input-property="inputProperty" />
    <button id="convert-button" @click="convertProperty">convert!</button>
    <h1>{{ formattedProperty }}</h1>
  </div>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";
import InputPropertyArea from "~/components/atoms/InputPropertyArea.vue";

interface CssProperty {
  property: string;
  value: string;
}

interface CssPropertyDictionary {
  [id: string]: CssProperty;
}

@Component({
  components: {
    InputPropertyArea
  }
})
export default class TopPage extends Vue {
  text: string = "";
  formattedProperty: string = "";

  convertProperty() {
    const cssPropertyDictionary: CssPropertyDictionary = this.createPropertyList();
    console.log(cssPropertyDictionary);

    const formattedProperty: string = this.formatProperty(cssPropertyDictionary);
    this.formattedProperty = formattedProperty;
  }

  inputProperty(value: string) {
    this.text = value;
  }

  createPropertyList(): CssPropertyDictionary {
    const cssPropertyDictionary: CssPropertyDictionary = {};
    const inputTexts = this.text.trim().split(";");
    inputTexts.forEach(text => {
      const value = text.trim().split(":");
      const cssProperty: CssProperty = {
        property: value[0],
        value: value[1]
      };
      cssPropertyDictionary[value[0]] = cssProperty;
    });
    return cssPropertyDictionary;
  }

  formatProperty(cssPropertyDictionary: CssPropertyDictionary): string {
    const top = cssPropertyDictionary["margin-top"];
    const right = cssPropertyDictionary["margin-right"];
    const bottom = cssPropertyDictionary["margin-bottom"];
    const left = cssPropertyDictionary["margin-left"];
    
    console.log(top);

    if (top && right && bottom && left) {
      return "margin: " + top.value + " " + right.value + " " + bottom.value + " " + left.value + ";"
    }

    return "";
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
