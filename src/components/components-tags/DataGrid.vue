<template>
  <div>
    <div class="modal">
      <div class="modal-block">
        <div class="modal-title">
          <h2>{{ modal_title }}</h2>
          <i class="bi bi-exclamation-triangle-fill"></i>
        </div>
        <div class="modal-content">
          <p>{{ modal_message }}</p>
          <div class="modal-buttons">
            <div v-on:click="modal_button_click" class="modal-button-yes modal-button">Yes</div>
            <div v-on:click="modal_button_click" class="modal-button-no modal-button">No</div>
          </div>
        </div>
      </div>
    </div>
    <table :id="id" class="data-grid">
      <thead class="head">
      <tr>
        <th>Actions</th>
        <th v-for="(header, index) in head" :key="index">
          {{ header }}
        </th>
      </tr>
      </thead>
      <tbody class="body">
        <tr v-for="(data, _index) in contentData" :key="_index">
          <td class="actions">
            <i class="bi bi-box-arrow-in-right"></i>
            <i class="bi bi-arrow-down-right-circle-fill"></i>
            <i class="bi bi-trash"></i>
          </td>
          <td v-for="(_data, __index) in data" :key="__index">
            {{ _data }}
          </td>
        </tr>
      </tbody>
    </table>
    <div v-if="contentData.length === 0" class="no-data">
      <DataGridSpinner id="Spinner" />
      No Data
    </div>
  </div>
</template>

<script>
import $ from "jquery";

import "../../styles/modal.css";
import DataGridSpinner from "./DataGridSpinner";

export default {
  name: "DataGrid",
  components: {DataGridSpinner},
  data () {
    return {
      head: ["Name", "Curso", "Continuation", "Status", "N° de Cursos"],
      contentData: [],
      modal_title: "Alert!",
      modal_message: "Are you sure?"

    }

  },
  watch: {

  },
  mounted() {
    $(".modal").hide();

    setTimeout(() => {
      $(".no-data").addClass("no-data-low-color");
      $("#Spinner").fadeIn(1500);
      $(".body").hide();

    }, 2000);

    setTimeout(() => {
      $(".no-data").removeClass("no-data-low-color");
      $("#Spinner").fadeOut(1500);

      this.contentData = [
        ["Algoritimo", "ENEM", "No", "Active", "9"],
        ["Algoritimo", "ENEM", "No", "Active", "9"],
        ["Algoritimo", "ENEM", "No", "Active", "9"],
        ["Algoritimo", "ENEM", "No", "Active", "9"],
        ["Algoritimo", "ENEM", "No", "Active", "9"],
        ["Algoritimo", "ENEM", "No", "Active", "9"],
        ["Algoritimo", "ENEM", "No", "Active", "9"],
        ["Algoritimo", "ENEM", "No", "Active", "9"],
        ["Algoritimo", "ENEM", "No", "Active", "9"],
        ["Algoritimo", "ENEM", "No", "Active", "9"],
        ["Algoritimo", "ENEM", "No", "Active", "9"],
      ];

      $(".body").fadeIn(2000);

    }, 5000);

    setTimeout(() => {
      $(".bi-trash").click(() => {
        this.modal_message = "Are you sure that you want delete this data?";
        $(".modal").fadeIn(1000);

      });

      $(".bi-arrow-down-right-circle-fill").click(() => {
        this.modal_message = "Are you sure that you want disable this data?";
        $(".modal").fadeIn(1000);

      });

    }, 5010);

    /*
    *
    * [
          ["Algoritimo", "ENEM", "No", "Active", "9"],
          ["Algoritimo", "ENEM", "No", "Active", "9"],
          ["Algoritimo", "ENEM", "No", "Active", "9"],
          ["Algoritimo", "ENEM", "No", "Active", "9"],
          ["Algoritimo", "ENEM", "No", "Active", "9"],
          ["Algoritimo", "ENEM", "No", "Active", "9"],
          ["Algoritimo", "ENEM", "No", "Active", "9"],
          ["Algoritimo", "ENEM", "No", "Active", "9"],
          ["Algoritimo", "ENEM", "No", "Active", "9"],
          ["Algoritimo", "ENEM", "No", "Active", "9"],
          ["Algoritimo", "ENEM", "No", "Active", "9"],
      ]
    *
    * */

  },
  props: {
    url_data: {
      type: String,
      required: true

    },
    name: {
      type: String,
      required: true

    },
    id: {
      type: String,
      required: true

    }
  },
  methods: {
    modal_button_click (ev) {
      const button = $(ev.target);

      if (button.text().toLowerCase() === "yes")
        console.log("");

      $(".modal").fadeOut(200);

    }

  }
}
</script>

<style scoped>
.no-data-low-color {
  background-color: #E9E9E9 !important;
  color: #BBB !important;

}

.no-data {
  width: auto;
  height: 70px;

  text-align: center;

  display: flex;

  justify-content: center;
  align-items: center;

  border-spacing: 2px;
  border: 2px solid #FFF;

  border-top: 0;
  border-bottom: 0;

  background-color: #EEE;

  color: #999;

  font-family: Calibri, sans-serif !important;
  font-size: 20px;

}

.actions {
  display: flex;

  justify-content: center;
  align-items: center;

}

.actions>i {
  font-size: 18px;

  transition: all .7s ease;

}

.actions>i:not(:first-child) {
  margin-left: 10px;

}

.actions>i:hover {
  cursor: pointer;

  transform: scale(1.4);

}

.bi-box-arrow-in-right {
  color: #A44EFA;

}

.bi-arrow-down-right-circle-fill {
  color: #FF1A1A;

}

.bi-trash {
  color: #FF4E1A;

}

.data-grid {
  width: 100%;
  height: 100%;

}

.head, .body {
  border-collapse: separate;
  text-decoration: none;
  text-align: center;

}

.head>tr>th, .body>tr>td {
  font-size: 20px;
  font-family: Calibri, sans-serif !important;

  padding-top: 5px;
  padding-bottom: 5px;

}

.body>tr>td {
  background-color: #FFF9F7;
  color: #000 !important;

  font-size: 15px !important;

  padding-bottom: 10px;
  padding-top: 10px;

}

.head>tr>th {
  background-color: #FF7B58;

  color: #FFF;

}

</style>