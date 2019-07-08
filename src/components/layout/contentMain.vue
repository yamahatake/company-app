<template>
  <main>
    <h1>Documents</h1>
    <filters @setStartDate="startDateFilter = $event" @setEndDate="endDateFilter = $event"/>
    <listResult :startDate="startDateFilter" :endDate="endDateFilter"/>
  </main>
</template>

<script>
import filters from '../filters';
import listResult from '../listResult';
export default {
  name: 'contentMain',
  data(){
    return{
      startDateFilter: '',
      endDateFilter: ''
    }
  },
  components: {
    'filters': filters,
    'listResult': listResult
  }
}
</script>