<template>

    <ul class="tab" :class="{[classPrefix+'-tabs']:classPrefix}">
      <li v-for="item in dataSource" :key="item.value"
          @click="tabSelect(item)"
          :class="tabList(item)"
          class="tab-item"
      >{{item.text}}

      </li>
    </ul>
</template>
<script lang="ts">
import Vue from 'vue';
import {Component, Prop} from 'vue-property-decorator';

type dataSourceItem={
  text:string,
  value:string
}

@Component
export default class Tabs extends Vue {
  @Prop({required:true,type:Array}) dataSource!:dataSourceItem[]
  @Prop(String) readonly value!: string;
  @Prop(String)  classPrefix?:string;

  tabList(item:dataSourceItem){
    return {
      [this.classPrefix+'-tabs-item']:this.classPrefix,
      selected:item.value===this.value
    }
  }

  tabSelect(item:dataSourceItem){
    this.$emit('update:value',item.value)
  }

}
</script>

<style lang="scss" scoped>
.tab {
  background: #c4c4c4;
  display: flex;
  text-align: center;
  font-size: 24px;
  &-item {
    width: 50%;
    height: 64px;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    &.selected::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      height: 4px;
      background: #333;
    }
  }
}

</style>