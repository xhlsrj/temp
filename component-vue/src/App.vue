<template>
  <div class="page">
    <div class="input-box">
      <BorderBox>
        <InputText v-model:value="value" />
      </BorderBox>
    </div>
    <br />
    <div class="input-box">
      <BorderBox>
        <InputFixBox />
      </BorderBox>
    </div>
    <br />
    <div class="dropdown-box">
      <DropdownBox>
        <div class="dropdown">dropdown</div>
        <template v-slot:panel>
          <div class="panel-box">
            <div class="panel">panel</div>
          </div>
        </template>
      </DropdownBox>
    </div>
    <div class="placeholder"></div>
    <div class="dropdown-box">
      <DropdownPanel>
        <div class="dropdown">dropdown panel</div>
        <template v-slot:panel>
          <div class="panel-box">
            <div class="panel">panel</div>
          </div>
        </template>
      </DropdownPanel>
    </div>
    <div class="placeholder"></div>

    <TabBar />
    <br />
    <DragBlock />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import InputText from './components/form/input/InputText.vue';
import BorderBox from './components/form/input/BorderBox.vue';
import InputFixBox from './components/form/input/InputFixBox.vue';
import DropdownBox from './components/form/dropdown/DropdownBox.FSM.vue';
import DropdownPanel from './components/form/dropdown/DropdownPanel.FSM.vue';
import TabBar from './components/tabbar/TabBar.vue';
import DragBlock from './components/drag/DragBlock.vue';

export default defineComponent({
  name: 'App',
  components: {
    InputText,
    BorderBox,
    InputFixBox,
    DropdownBox,
    DropdownPanel,
    TabBar,
    DragBlock,
  },
  data() {
    return {
      value: ``,
    };
  },
});
</script>
<style>
@import './style/reset.css';
@import './style/lib.css';
</style>
<style scoped>
.page {
  padding: 100px;
}
.input-box {
  font-size: 20px;
  width: 400px;
  height: 40px;
}
.placeholder {
  height: 100px;
}

.dropdown-box {
  width: 300px;
}
.dropdown {
  height: 30px;
  border: 1px solid #000;
  cursor: pointer;
  user-select: none;
}
.panel-box {
  position: relative;
}
.panel {
  position: absolute;
  width: 100%;
  height: 30px;
  border: 1px solid #000;
  box-sizing: border-box;
}
</style>
