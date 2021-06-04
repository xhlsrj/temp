<template>
  <div class="box">
    <div
      v-for="tab in tabArr"
      :key="tab.value"
      class="tab"
      :class="{ current: tabState.matches(tab.value) }"
      @click="tabSwitch('SELECT_' + tab.value)"
    >
      {{ tab.text }}
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { createMachine, assign } from 'xstate';
import { useMachine } from '@xstate/vue';

export default defineComponent({
  name: 'TabBar',
  setup: () => {
    const SELECT_T1 = `T1`,
      SELECT_T2 = `T2`,
      SELECT_T3 = `T3`,
      SELECT_T4 = `T4`,
      SELECT_T5 = `T5`;
    const switchMachine = createMachine({
      id: `tab`,
      initial: `T1`,
      states: {
        T1: {
          on: {
            SELECT_T2,
            SELECT_T3,
            SELECT_T4,
            SELECT_T5,
          },
        },
        T2: {
          on: {
            SELECT_T1,
            SELECT_T3,
            SELECT_T4,
            SELECT_T5,
          },
        },
        T3: {
          on: {
            SELECT_T1,
            SELECT_T2,
            SELECT_T4,
            SELECT_T5,
          },
        },
        T4: {
          on: {
            SELECT_T1,
            SELECT_T2,
            SELECT_T3,
            SELECT_T5,
          },
        },
        T5: {
          on: {
            SELECT_T1,
            SELECT_T2,
            SELECT_T3,
            SELECT_T4,
          },
        },
      },
    });
    const tfsm = useMachine(switchMachine);
    const { state: tabState, send: tabSwitch } = tfsm;
    return {
      tabArr: [
        { value: `T1`, text: `1` },
        { value: `T2`, text: `2` },
        { value: `T3`, text: `3` },
        { value: `T4`, text: `4` },
        { value: `T5`, text: `5` },
      ],
      tfsm,
      tabState,
      tabSwitch,
    };
  },
  data() {
    return {
      currentTab: `1`,
    };
  },
  methods: {
    click(tab: { value: string }) {
      this.currentTab = tab.value;
    },
  },
});
</script>

<style scoped>
.box {
  display: flex;
}
.tab {
  width: 100px;
  height: 50px;
  border: 2px solid #000;
  border-right: none;
}
.tab:last-child {
  border-right: 2px solid #000;
}

.tab.current {
  border: 2px solid skyblue;
}
.current + .tab {
  border-left: none;
}
</style>
