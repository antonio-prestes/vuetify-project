<template>
  <v-menu
    :close-on-content-click="false"
  >
    <template v-slot:activator="{ props }">
      <v-btn
        color="primary"
        v-bind="props"
        variant="outlined"
        width="500px"
      >
        Dropdown
      </v-btn>
    </template>
    <div class="bg-white px-5 pt-2">
      <v-text-field
        v-model="search"
        variant="outlined"
        density="compact"
        append-inner-icon="mdi-magnify"
        single-line
        hide-details
        @keyup="filter"
      ></v-text-field>
    </div>
    <div>
      <v-list
        max-height="300px"
      >
        <v-list-item
          v-for="(item, index) in itemsList"
          height="50px"
          :key="index"
        >
          <v-checkbox
            v-model="itemsSelected"
            :label="item.name"
            :value="item"
          />
        </v-list-item>
      </v-list>
    </div>
    <div class="bg-white px-4 d-flex justify-between">
      <v-btn color="#5865f2" @click="clearSelection">
        Limpar
      </v-btn>
      <v-btn color="#5865f2" @click="selectItems">
        Selecionar
      </v-btn>
    </div>
  </v-menu>
</template>
<script>
export default {
  name: 'DropDownSelect',
  props: {
    people: {
      type: Array,
      default: () => {
        []
      }
    }
  },
  data() {
    return {
      itemsSelected: [],
      filtrado: [],
      search: '',
    }
  },
  computed: {
    itemsList() {
      return this.filtrado.length > 0 ? this.filtrado : this.people;
    }
  },
  methods: {
    clearSelection() {
      this.itemsSelected = [];
      this.$emit('clear-selection');
    },
    selectItems() {
      this.$emit('selected-items-changed', this.itemsSelected);
    },
    filter() {
      return this.filtrado = this.people.filter(item =>
        item.name.toLowerCase().includes(this.search.toLowerCase())
      );
    },
  },
}
</script>
