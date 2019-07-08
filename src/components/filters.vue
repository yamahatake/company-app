<template>
  <aside id="listFilter">
    <form>
      <p>Filter by</p>
      <input type="date" id="fromDate" name="fromDate" pattern="[0-9]{4}-[0-9]{2}-[0-9]{2}" min="1990-01-01" max="2020-01-01" placeholder="From" v-model="startDateFilter"/>
      <input type="date" id="toDate" name="toDate" pattern="[0-9]{4}-[0-9]{2}-[0-9]{2}" min="1990-01-01" max="2020-01-01" placeholder="To" v-model="endDateFilter"/>
      <button id="applyFilters" @click="applyDates()">Apply filters</button>
      <button id="clearFilters" @click="clearDates()">Clear Filters</button>
    </form>
  </aside>
</template>

<script>
export default {
  name: 'filters',
  data(){
    return{
      startDateFilter: '',
      endDateFilter: ''
    }
  },
  methods: {
    dateGMT(date){
      let year = date.substring(0,4);
      let month = date.substring(5,7);
      let day = date.substring(8,11);
      return new Date(year,month-1,day).toLocaleDateString();
    },
    applyDates(){
      event.preventDefault();
      this.$emit('setStartDate', this.dateGMT(this.startDateFilter));
      this.$emit('setEndDate', this.dateGMT(this.endDateFilter));
    },
    clearDates(){
      event.preventDefault()
      this.$emit('setStartDate', '');
      this.startDateFilter = '';
      this.$emit('setEndDate', '');
      this.endDateFilter = '';
    }
  }
}
</script>