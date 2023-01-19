<template>
  <div class="card">
    <div class="card-header" v-if="$slots.title">
      <slot name="title"></slot>
    </div>
    <div class="card-body">
      <div class="row mb-3">
        <div class="col-md-12">
          <div class="form-inline justify-content-end">
            <div class="form-group">
              <data-search v-model="searchTerm"></data-search>
            </div>
          </div>
        </div>
      </div>

      <app-alert
        message="No products found!"
        type="danger"
        v-if="!records.length"
      >
        <i class="fa fa-exclamation-triangle"></i>
      </app-alert>

      <table v-else class="table table-striped table-hover">
        <thead>
          <slot name="head"></slot>
        </thead>
        <tbody>
          <slot name="body" :records="recordsFiltered"></slot>
        </tbody>
      </table>
    </div>
    <div class="card-footer">
      <nav>
        <ul class="pagination justify-content-center">
          <li class="page-item disabled">
            <a class="page-link" href="#">Previous</a>
          </li>
          <li class="page-item" v-for="page in pages" :key="`page-${page}`">
            <a class="page-link" href="#">{{ page }}</a>
          </li>
          <li class="page-item"><a class="page-link" href="#">Next</a></li>
        </ul>
      </nav>
    </div>
  </div>
</template>

<script>
import DataSearch from "./DataSearch.vue";

export default {
  props: {
    searchKey: {
      type: String,
      default: "name",
    },
  },
  components: {
    DataSearch,
  },
  created() {
    console.log(this.$slots);
  },
  data() {
    return {
      records: [
        {
          id: 1,
          name: "Intelligent Granite Table",
          category: "Tools",
          price: "787.00",
        },
        {
          id: 2,
          name: "Handcrafted Rubber Hat",
          category: "Games",
          price: "232.00",
        },
        {
          id: 3,
          name: "Rustic Concrete Salad",
          category: "Jewelery",
          price: "115.00",
        },
        {
          id: 4,
          name: "Gorgeous Concrete Pizza",
          category: "Garden",
          price: "250.00",
        },
        {
          id: 5,
          name: "Refined Plastic Shoes",
          category: "Health",
          price: "844.00",
        },
        {
          id: 6,
          name: "Awesome Metal Soap",
          category: "Tools",
          price: "326.00",
        },
        {
          id: 7,
          name: "Intelligent Fresh Mouse",
          category: "Home",
          price: "783.00",
        },
        {
          id: 8,
          name: "Licensed Soft Keyboard",
          category: "Music",
          price: "361.00",
        },
        {
          id: 9,
          name: "Fantastic Rubber Pants",
          category: "Garden",
          price: "786.00",
        },
        {
          id: 10,
          name: "Awesome Rubber Ball",
          category: "Automotive",
          price: "696.00",
        },
      ],
      pages: 3,
      searchTerm: "",
    };
  },
  computed: {
    recordsFiltered() {
      if (!this.searchTerm) {
        return this.records;
      }

      return this.records.filter((record) =>
        record[this.searchKey].match(new RegExp(this.searchTerm, "i"))
      );
    },
  },
};
</script>
