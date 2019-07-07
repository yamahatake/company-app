<template>
  <article id="listDocuments">
    <table>
      <thead>
        <th>Document Name</th>
        <th>Date</th>
      </thead>
      <tbody>
        <tr>
          <td>Document</td>
          <td>05-06-2018</td>
        </tr>
        <tr>
          <td>Document</td>
          <td>05-06-2018</td>
        </tr>
        <tr>
          <td>Document</td>
          <td>05-06-2018</td>
        </tr>
      </tbody>
      <tfoot>
        <td colspan="2">
          <pagination/>
        </td>
      </tfoot>
    </table>
  </article>
</template>

<script>
import pagination from './uiElements/pagination.vue'
export default {
  name: 'listResult',
  components: {'pagination':pagination}
}
</script>