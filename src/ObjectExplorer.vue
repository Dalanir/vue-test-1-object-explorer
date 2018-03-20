<template>
  <div class="object-explorer">
    <div
      v-for="el in keys"
      :key="el"
    >
      <div>
        {{ el }}
        <span v-if="isObject(el)" @click="toggleChidlrenVisibility">
          <span v-if="childrenAreVisible"> - </span>
          <span v-else> + </span>
        </span>
        <span v-else> : </span>
      </div>
      <div v-if="isObject(el)">
        <object-explorer v-show="childrenAreVisible" :obj="obj[el]"></object-explorer>
      </div>
      <div v-else> {{ obj[el] }} </div>
    </div>
  </div>
</template>

<script>
import _ from 'lodash';

export default {
  name: 'object-explorer',
  props: ['obj'],
  data() {
    return {
      childrenAreVisible: false
    }
  },
  computed: {
    keys() {
      const keys = _.keys(this.obj);
      console.log(keys);
      return keys;
    },
  },
  methods: {
    isObject(el) {
      return _.isObject(this.obj[el])
    },
    toggleChidlrenVisibility() {
      return this.childrenAreVisible = !this.childrenAreVisible;
    }
  },
}
</script>
