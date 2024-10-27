<template>
  <div class="container">
    <h1 class="text-2xl bold my-4">Integrated Information Processing Model</h1>
    <iip-model :input-adequacy="activeScenario.properties.inputAdequacy"
               :reference-consonance="activeScenario.properties.referenceConsonance"
               :output-diagnosticity="activeScenario.properties.outputDiagnosticity"  />
  </div>
</template>

<script>
import IipModel from "@/components/iip-model.vue";
export default {
  name: "iip-simulator",
  components: {IipModel},
  data () {
    return {
      scenarios: {
        'demo' : {
          properties: {
            inputAdequacy: true,
            referenceConsonance: false,
            outputDiagnosticity: false,
          }
        },
        'demo2' : {
          properties: {
            inputAdequacy: true,
            referenceConsonance: true,
            outputDiagnosticity: true,
          }
        },
      },
      activeScenario: JSON
    }
  },
  created() {
    this.activeScenario = this.scenarios.demo2;
  }
}
</script>

<style scoped>

</style>