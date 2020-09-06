<template>
  <div class="wrapper">
    <div class="container">
      <header class="header">
        <h1>Pantone colors</h1>
        <span :class="{active: statusResetBtn}" @click="resetForm">Reset</span>
      </header>
      <main class="main">
        <HeadTable :visibleColumn="visibleColumn" @changeVisibleColumn="changeVisibleColumn" />
        <div class="bodyTable">
          <TableRow 
          v-for="(item, index) of this.dataAjax" 
          :key="index" 
          :item="item" 
          :visibleColumn="visibleColumn"
          @changeVisibleColumn="changeVisibleColumn"
          />
        </div>
      </main>
    </div>
  </div>
</template>

<script>
import HeadTable from "./HeadTable.vue";
import TableRow from "./TableRow.vue";
import $ from "jquery";

export default {
  name: "App",
  components: {
    HeadTable,
    TableRow,
  },
  data() {
    return {
      dataAjax: [],
      visibleColumn: {
        id: true,
        name: true,
        year: true,
        color: true,
        pantone: true,
      },
      statusResetBtn: false,
    };
  },
  props: {},

  methods: {
    init() {
      if (typeof localStorage.id == "undefined") {
        for (let [key, value] of Object.entries(this.visibleColumn)) {
          localStorage.setItem(key, value);
        }
      } else {
        for (let [key, value] of Object.entries(localStorage)) {
          if (value == "true") {
            this.visibleColumn[key] = true;
          } else if (value == "false") {
            this.visibleColumn[key] = false;
          }
        }
        this.statusResetBtn = localStorage.getItem("statusResetBtn");
      }
    },
    changeVisibleColumn(columnName) {
      localStorage.setItem(columnName, false);
      localStorage.setItem("statusResetBtn", false);

      this.statusResetBtn = true;
    },
    ajax: function() {
      let _this = this;
      $.ajax({
        url: "https://reqres.in/api/unknown?per_page=12",
        success: function(data) {
          console.log(data);
          _this.dataAjax = data.data;
        },
        error: function(error) {
          console.log("Ajax error: ", error);
        },
      });
    },
    resetForm() {
      this.statusResetBtn = false;
      for (let key of Object.keys(this.visibleColumn)) {
        this.visibleColumn[key] = true;
      }
      localStorage.clear();
    },
  },
  beforeMount() {
    this.ajax();
    this.init();
  },
};
</script>

