<template>
  <div>
    <textarea
      rows="5"
      @input="$emit('input-property', $event.target.value)"
    ></textarea>
  </div>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";

@Component({})
export default class InputPropertyArea extends Vue {}
</script>
