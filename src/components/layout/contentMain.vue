<template>
  <main>
    <h1>Documents</h1>
    <filters/>
    <listResult/>
  </main>
</template>

<script>
import filters from '../filters';
import listResult from '../listResult';
export default {
  name: 'contentMain',
  components: {
    'filters': filters,
    'listResult': listResult
  }
}
</script>