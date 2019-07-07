<template>
  <aside id="listFilter">
    <form>
      <p>Filter by</p>
      <input type="date" id="fromDate" name="fromDate" pattern="[0-9]{4}-[0-9]{2}-[0-9]{2}" min="1990-01-01" max="2020-01-01"/>
      <input type="date" id="toDate" name="toDate" pattern="[0-9]{4}-[0-9]{2}-[0-9]{2}" min="1990-01-01" max="2020-01-01"/>
      <button id="applyFilters">Apply filters</button>
      <button id="clearFilters">Clear Filters</button>
    </form>
  </aside>
</template>

<script>
export default {
  name: 'filters'
}
</script>