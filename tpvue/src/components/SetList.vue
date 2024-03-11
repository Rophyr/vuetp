<!-- SetList.vue -->
<template>
  <div>
    <h2>Sets</h2>
    <ul>
      <li v-for="set in sets" :key="set.code">
        {{ set.name }} - {{ set.code }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    sets: Array
  }
}
</script>
