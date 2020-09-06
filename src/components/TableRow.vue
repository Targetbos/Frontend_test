<template>
  <div class="row">
    <div class="cell id" v-if="visibleColumn.id"><span>{{ item.id }}</span></div>
    <div class="cell name" v-if="visibleColumn.name"><span>{{ item.name }}</span></div>
    <div class="cell year" v-if="visibleColumn.year"><span>{{ item.year}}</span></div>
    <div class="cell color" v-if="visibleColumn.color"><i :style="{background: item.color}"></i><span>{{ item.color }}</span></div>
    <div class="cell pantone" v-if="visibleColumn.pantone"><span>{{ item.pantone_value }}</span></div>
  </div>
</template>

<script>
export default {
  name: "TableRow",
  props: {
    item: Object,
    visibleColumn: Object,
  },
  data() {
    return {};
  },
};
</script>
