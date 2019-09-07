<template>
  <aside id="listFilter">
    <div id="wrapper-filter">
      <form :class="{'active': mobileToggle == false}">
        <p>Filter by</p>
        <a class="close" @click="toggleFilter()"></a>
        <datepicker id="fromDate" :format="formatDate" placeholder="From" v-model="startDateFilter"/>
        <datepicker id="toDate" :format="formatDate" placeholder="To" v-model="endDateFilter"/>
        <button id="applyFilters" @click="applyDates()">Apply filters</button>
        <button id="clearFilters" @click="clearDates()">Clear Filters</button>
      </form>
      <a @click="toggleFilter()" :class="{'active': mobileToggle == true}" v-if="mobileToggle">Filter by</a>
    </div>
  </aside>
</template>

<script>
import Datepicker from 'vuejs-datepicker';

export default {
  name: 'filters',
  data(){
    return{
      startDateFilter: '',
      endDateFilter: '',
      formatDate: "dd/MM/yyyy",
      mobileToggle: true
    }
  },
  components: {'Datepicker': Datepicker},
  methods: {
    convertDate(date){
      return date.toJSON();
    },
    applyDates(){
      event.preventDefault();
      this.startDateFilter ? this.$emit('setStartDate', this.convertDate(this.startDateFilter)) : null;
      this.endDateFilter ? this.$emit('setEndDate', this.convertDate(this.endDateFilter)): null;
    },
    clearDates(){
      event.preventDefault()
      this.$emit('setStartDate', '');
      this.startDateFilter = '';
      this.$emit('setEndDate', '');
      this.endDateFilter = '';
    },
    toggleFilter(){
      this.mobileToggle = !this.mobileToggle;
    }
  }
}
</script>