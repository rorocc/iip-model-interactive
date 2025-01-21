<template>
  <div class="container">
    <h1 class="text-2xl bold my-4">Integrated Information Processing Model</h1>
    <div class="my-4">
      <label for="categories">Select a scenario:</label>
      <select class="py-2 px-2 mx-4 bg-gray-100 rounded-lg border"
              v-model="this.activeScenario"
              name="categories" id="categories">
        <option disabled value="">Select a Scenario</option>
        <option v-for="scenario in scenarios" :value="scenario">{{scenario.name}}</option>
      </select>
    </div>

    <div class="relative">
      <div class="absolute w-full">
        <iip-model :input-adequacy="activeScenario.properties.inputAdequacy"
                   :reference-consonance="activeScenario.properties.referenceConsonance"
                   :output-diagnosticity="activeScenario.properties.outputDiagnosticity"  />
      </div>
      <iip-model-input-adequacy v-show="isSubloopInputAdequacyVisible" class="absolute left-0"/>
      <iip-model-output-diagnosticity v-show="isSubloopOutputDiagnosticityVisible" class="absolute right-0" />
      <iip-model-reference-consonance v-show="isSubloopReferenceConsonanceVisible" class="absolute right-1/4"/>
    </div>
  </div>
  <div id="tooltips-container">
    <tooltip v-if="activeScenario.tooltips"  v-for="tooltip in activeScenario.tooltips"
             class="hidden"
             v-on.once="this.registerTooltipById(tooltip.tooltipId, tooltip.targetId)"
             :id="tooltip.tooltipId"
             :headline="tooltip.headline"
             :text="tooltip.text"
    />
    <tooltip v-for="tooltip in tooltips"
              class="hidden"
             :id="tooltip.tooltipId"
             :headline="tooltip.headline"
             :text="tooltip.text"
    />
  </div>
</template>

<script>
import IipModel from "@/components/iip-model.vue";
import Tooltip from "@/components/tooltip.vue";
import IipModelInputAdequacy from "@/components/iip-model-input-adequacy.vue";
import IipModelOutputDiagnosticity from "@/components/iip-model-output-diagnosticity.vue";
import IipModelReferenceConsonance from "@/components/iip-model-reference-consonance.vue";
import tooltips from "@/assets/tooltips.json";
import scenarios from "@/assets/scenarios.json"
export default {
  name: "iip-simulator",
  components: {IipModelReferenceConsonance, IipModelOutputDiagnosticity, IipModelInputAdequacy, Tooltip, IipModel},
  data () {
    return {
      tooltips: tooltips,
      isSubloopInputAdequacyVisible: false,
      isSubloopOutputDiagnosticityVisible: false,
      isSubloopReferenceConsonanceVisible: false,
      scenarios: scenarios,
      activeScenario: JSON
    }
  },
  created() {
    this.activeScenario = this.scenarios[0];
  },
  methods: {
    registerTooltipById(tooltipId, targetId) {
      document.getElementById(targetId).onmousemove = (evt) => {
        this.showTooltip(tooltipId, evt)
      };
      document.getElementById(targetId).onmouseout = () => {
        this.hideTooltip(tooltipId)
      };
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
    // registering all tooltips from /assets/tooltips.json
    tooltips.forEach((tooltip) => {
      this.registerTooltipById(tooltip.tooltipId, tooltip.targetId)
    })

    document.getElementById("Container-InputAdequacy").onclick = () => {this.isSubloopInputAdequacyVisible = true}
    document.getElementById("closeSubloopInputAdequacy").onclick = () => {this.isSubloopInputAdequacyVisible = false}

    document.getElementById("Container-OutputDiagnosticity").onclick = () => {this.isSubloopOutputDiagnosticityVisible = true}
    document.getElementById("closeSubloopOutputDiagnosticity").onclick = () => {this.isSubloopOutputDiagnosticityVisible = false}

    document.getElementById("Container-ReferenceConsonance").onclick = () => {this.isSubloopReferenceConsonanceVisible = true}
    document.getElementById("closeSubloopReferenceConsonance").onclick = () => {this.isSubloopReferenceConsonanceVisible = false}
  }
}
</script>

<style scoped>

</style>