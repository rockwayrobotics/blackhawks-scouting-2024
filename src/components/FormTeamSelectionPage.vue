<template>
  <FormPage title="Team Selection" ref="page">
    <FormGroup :label-type="LabelType.LabelTag" id="match-input" name="Match Number">
      <input id="match-input" type="number" v-model.lazy="matchNumber" :min="1" />
    </FormGroup>
    <FormGroup :label-type="LabelType.LabelTag" id="team-number-input" name="Team Number">
      <input type="number" v-model="teamNumberManual">
    </FormGroup>
    <FormGroup :label-type="LabelType.LabelTag" id="team-color-input" name="Team Color">
      <select id="team-color-input" v-model="teamColorManual">
        <option value="Red" selected>Red</option>
        <option value="Blue">Blue</option>
      </select>
    </FormGroup>
  </FormPage>
</template>

<script setup lang="ts">
import FormGroup from "./FormGroup.vue";
import FormPage from "./FormPage.vue";
import { LabelType } from "@/common/shared";
import { computed } from "vue";
import { useWidgetsStore } from "@/common/stores";

const page = $ref<InstanceType<typeof FormPage>>();
defineExpose({ title: computed(() => page?.title), setShown: computed(() => page?.setShown) });

const widgets = useWidgetsStore();

const matchNumber = $ref(1);

const teamNumberManual = $ref(0);
const teamColorManual = $ref("Red");

// The exported team information
const teamData = $computed(() => {
  return `${teamNumberManual}`;
});

const teamColor = $computed(() => {
  return `${teamColorManual}`;
});

// Add values to export
widgets.addWidgetValue("MatchNumber", $$(matchNumber));
widgets.addWidgetValue("TeamColor", $$(teamColor));
widgets.addWidgetValue("Team", $$(teamData));
</script>

<style>
#team-input {
  width: 250px;
  text-overflow: ellipsis;
}
</style>
