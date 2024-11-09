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

    <tooltip id="tooltip-comparator" headline="Comparator" text="The comparator continuously assesses the input against the reference value, triggering adjustments in the output function when discrepancies are detected." />
    <tooltip id="tooltip-reference" headline="Reference Function" text="The reference function contains all processes and target values used to analyze the input information." />
    <tooltip id="tooltip-input" headline="Input Function" text="The available machine data and human information represent the overall input for information processing, which means that anything that is not part of the human information or machine data is not processed." />
  </div>
</template>

<script>
import IipModel from "@/components/iip-model.vue";
import Tooltip from "@/components/tooltip.vue";
export default {
  name: "iip-simulator",
  components: {Tooltip, IipModel},
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
    },
    showTooltip(tooltipId, evt) {
      let tooltip = document.getElementById(tooltipId);
      tooltip.style.display = "block";
      tooltip.style.left = evt.pageX + 16 + "px";
      tooltip.style.top = evt.pageY + "px";
    },
    hideTooltip(tooltipId){
      document.getElementById(tooltipId).style.display = "none";
    }
  },
  mounted() {
    // registering EFFECT tooltip events
    document.getElementById("Container-Goal-Reference").onmousemove = (evt) => {this.showTooltip("tooltip-reference",evt)};
    document.getElementById("Container-Goal-Reference").onmouseout = () => {this.hideTooltip("tooltip-reference")};

    // registering COMPARATOR tooltip events
    document.getElementById("Container-Comparator").onmousemove = (evt) => {this.showTooltip("tooltip-comparator",evt)};
    document.getElementById("Container-Comparator").onmouseout = () => {this.hideTooltip("tooltip-comparator")};

    // registering COMPARATOR tooltip events
    document.getElementById("Container-InputFunction").onmousemove = (evt) => {this.showTooltip("tooltip-input",evt)};
    document.getElementById("Container-InputFunction").onmouseout = () => {this.hideTooltip("tooltip-input")};
  }
}
</script>

<style scoped>

</style>