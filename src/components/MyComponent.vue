<template>
  <div class="q-pa-md">
    <q-btn
      color="primary"
      :label="options ? visibleOption : unvisibleOption"
      @click="showOptions()"
    />
    <span v-if="options">
      <div class="labelOption">Choose separator for table:</div>
      <q-option-group
        v-model="separator"
        inline
        :options="[
          { label: 'Horizontal', value: 'horizontal' },
          { label: 'Vertical', value: 'vertical' },
          { label: 'Cell', value: 'cell' },
          { label: 'None', value: 'none' },
        ]"
      />
      <div class="labelOption">Choose theme for table:</div>
      <q-option-group
        v-model="dark"
        inline
        :options="[
          { label: 'Dark', value: 'dark' },
          { label: 'Light', value: 'light' },
        ]"
      />
    </span>
    <q-table
      :title="title"
      :rows="rows"
      :columns="columnsFunction()"
      row-key="name"
      :separator="separator"
      :dark="dark"
      bordered
      selection="single"
      v-model:selected="selected"
      :grid="this.$q.screen.width > 1023 ? false : true"
    />

    <div className="selectedItem" v-if="selected">
      {{ showSelected(selected) }}
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import { rows } from './tablerows';

export default defineComponent({
  name: 'MyComponent',
  data() {
    return {
      title: 'Deserts',
      rows,
      separator: ref('vertical'),
      dark: ref('dark'),
      selected: ref([]),
      options: true,
      visibleOption: 'Hide options',
      unvisibleOption: 'Show options',
    };
  },
  methods: {
    showSelected(param: any) {
      let elements = '';
      param.forEach((item: any) => {
        const array = Object.entries(item);
        for (let element of array) {
          elements += element[0].toUpperCase() + ': ' + element[1] + ', ';
        }
      });
      return elements;
    },
    columnsFunction() {
      return Object.keys(rows[0]).map((columnName) => {
        return {
          name: columnName,
          label: columnName,
          align: 'left',
          sortable: true,
          field: columnName,
        };
      });
    },
    showOptions() {
      this.options = !this.options;
    },
  },
});
</script>
