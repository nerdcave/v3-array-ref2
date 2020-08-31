<template>
  <div id="app">
    itemsSorted: {{ itemsSorted }}
    <br>
    countPlus1: {{ countPlus1 }}
    <hr/>
    <br>
    items: {{ items }}<br>
    count: {{ count }}<br>
    <button @click="items.push(Math.round(100*Math.random()))">add items</button>
    <button @click="count++">inc count</button>
    <br>
    <p>itemsSorted is triggered, countPlus1 is not.</p>
  </div>
</template>

<script>
/* eslint-disable */
import { ref, toRef, reactive, computed } from "vue";

export default {
  setup() {
    const items = ref([1, 2, 3])
    const count = ref(0)

    const state = reactive({ items, count })

    // does trigger itemsSorted computed but is this expected?
    // I expect it should be toRef(state, 'items')
    const itemsRef = ref(state.items)

    // does not trigger computed (as expected), but toRef(state, 'count') does
    const countRef = ref(state.count)
    // const countRef = toRef(state, 'count')

    const itemsSorted = computed(() => [...itemsRef.value].sort())
    const countPlus1 = computed(() => countRef.value + 1)

    return {items, count, itemsSorted, countPlus1}
  }
};
</script>
