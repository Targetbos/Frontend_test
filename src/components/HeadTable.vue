<template>
  <div class="headTable">
    <div class="row">
      <div class="cell id" v-show="visibleColumn.id">
        <label>ID
          <input type="checkbox" name="id" v-model="visibleColumn.id" @click="changeVisibleColumn">
        </label>
      </div>
      <div class="cell name" v-show="visibleColumn.name">
        <label>NAME
          <input type="checkbox" name="name" v-model="visibleColumn.name" @click="changeVisibleColumn">
        </label>
      </div>
      <div class="cell year" v-show="visibleColumn.year">
        <label>YEAR
          <input type="checkbox" name="year" v-model="visibleColumn.year" @click="changeVisibleColumn">
        </label>
      </div>
      <div class="cell color" v-show="visibleColumn.color">
        <label>COLOR
          <input type="checkbox" name="color" v-model="visibleColumn.color" @click="changeVisibleColumn">
        </label>
      </div>
      <div class="cell pantone" v-show="visibleColumn.pantone">
        <label>PANTONE
          <input type="checkbox" name="pantone" v-model="visibleColumn.pantone" @click="changeVisibleColumn">
        </label>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HeadTable",
  data() {
    return {};
  },
  props: { visibleColumn: Object },
  methods: {
    changeVisibleColumn(event) {
      this.$emit("changeVisibleColumn", event.target.name);
    },
  },
};
</script>

