<template>
  <article id="listDocuments">
    <table>
      <thead>
        <th @click="sortBy('name')" :class="{reverse: reverse, 'active': sortActive == 'name'}">
          Document Name <span><img src="../assets/images/icon-sort-gray.png"/></span>
        </th>
        <th @click="sortBy('date')" :class="{reverse: reverse, 'active': sortActive == 'date'}">
          Date <span><img src="../assets/images/icon-sort-gray.png"/></span>
        </th>
      </thead>
      <tbody>
        <tr v-for="(document, i) in filteredList" :key="i">
          <td>{{document.name}}</td>
          <td>{{document.date | formatDate}}</td>
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
import pagination from './uiElements/pagination.vue';
import axios from 'axios';
import _ from 'lodash';

export default {
  name: 'listResult',
  components: {'pagination':pagination},
  data() {
    return{
      documentList: [],
      currentPage: 1,
      reverse: false,
      sortActive: 'name'
    }
  },
  filters: {
    formatDate: (date) => {
      let format = new Date (date);
      return `${("0" + format.getDate()).slice(-2)}-${("0" + (format.getMonth() + 1)).slice(-2)}-${format.getFullYear()}`;
    }
  },
  methods: {
    sortBy(sort){
      this.reverse = !this.reverse;
      this.sortActive = sort;
      this.documentList = _.orderBy(this.documentList, sort, this.reverse ? 'asc' : 'desc');
    }
  },
  mounted(){
    let proxyUrl = 'https://cors-anywhere.herokuapp.com/';
    axios.get(`${proxyUrl}https://apply.crosslend.io/documents`)
    .then(response => {
      this.documentList = response.data.documents;
    })
    .catch(error => {
      console.log(error);
    })
  },
  computed: {
    filteredList() {
      return this.documentList.filter(item => {
        return item.name.includes('.pdf') || item.name.includes('.docx')
      })
    }
  }
}
</script>