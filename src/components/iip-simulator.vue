<template>
  <div class="container">
    <h1 class="text-2xl bold my-4">Integrated Information Processing Model</h1>
    {{this.scenariosOfCategory}}
    <label for="categories">Scenario Category</label>
    <select class="py-2 px-2 mx-4 bg-gray-100 rounded-lg border"
            v-model="this.selectedScenarioCategory"
            v-on:change="this.findScenariosByCategory(this.selectedScenarioCategory)"
            name="categories" id="categories">
      <option v-for="category in this.scenarioCategories" :value="category.id">{{category.name }}</option>
    </select>
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
      selectedScenarioCategory: 0,
      scenariosOfCategory: [],
      selectedScenario: 'demo',
      scenarioCategories:[
        {id:0, name: "AID"},
        {id:1, name: "DemoCat"},
        {id:2, name: "DemoDog"}
      ],
      scenarios: {
        'demo' : {
          categoryId: 0,
          properties: {
            inputAdequacy: true,
            referenceConsonance: false,
            outputDiagnosticity: false,
          }
        },
        'demo2' : {
          properties: {
            categoryId: 1,
            inputAdequacy: true,
            referenceConsonance: true,
            outputDiagnosticity: true,
          }
        },
        'demo3' : {
          properties: {
            categoryId: 2,
            inputAdequacy: true,
            referenceConsonance: false,
            outputDiagnosticity: true,
          }
        },
      },
      activeScenario: JSON
    }
  },
  created() {
    this.activeScenario = this.scenarios.demo2;
  },
  methods: {
    findScenariosByCategory(category){
      this.scenariosOfCategory = [];
      for (let i in this.scenarios) {
        if(this.scenarios[i].categoryId === category){
          this.scenariosOfCategory.push(this.scenarios[i]);
        }
      }
    }
  }
}
</script>

<style scoped>

</style>