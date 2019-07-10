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
          <td width="30%">{{document.date | formatDate}}</td>
        </tr>
      </tbody>
      <tfoot>
        <td colspan="2">
          <section class="pagination">
            <a class="fisrtPage" v-if="page != 1" @click="page= 1">&lt;&lt;</a>
            <a class="backPage" v-if="page != 1" @click="page--">&lt;</a>
            <span>{{page}} of {{pages}}</span>
            <a class="fowardPage" v-if="page < pages" @click="page++">&gt;</a>
            <a class="lastPage" v-if="page < pages" @click="page = pages">&gt;&gt;</a>
          </section>
        </td>
      </tfoot>
    </table>
    <p v-if="pages === 0">No results fould</p>
  </article>
</template>

<script>
import axios from 'axios';
import _ from 'lodash';

export default {
  name: 'listResult',
  props: ['startDate', 'endDate'],
  data() {
    return{
      documentList: [],
      listLength: 0,
      currentPage: 1,
      reverse: true,
      sortActive: 'date',
      page: 1,
      perPage: 6,
      pages: 0
    }
  },
  methods: {
    sortBy(sort){
      this.reverse = !this.reverse;
      this.sortActive = sort;
      this.documentList = _.orderBy(this.documentList, sort, this.reverse ? 'asc' : 'desc');
    },
    setPages() {
      this.pages = Math.ceil(this.listLength / this.perPage);
    },
    paginate(item) {
      let page = this.page;
      let perPage = this.perPage;
      let from = (page * perPage) - perPage;
      let to = (page * perPage);
      return item.slice(from, to);
    }
  },
  filters: {
    formatDate: (date) => {
      const year = date.substring(0,4);
      const month = date.substring(5,7);
      const day = date.substring(8,10);
      return`${day}-${month}-${year}`;
    }
  },
  created(){
    const proxyUrl = 'https://cors-anywhere.herokuapp.com/';
    axios.get(`${proxyUrl}https://apply.crosslend.io/documents`)
    .then(response => {
      const list = response.data.documents.filter(item => {
        return item.name.includes('.pdf') || item.name.includes('.docx')
      });
      this.documentList = list;
      this.sortBy('date');
    })
  },
  computed: {
    filteredList() {
      const filterDate = this.documentList.filter(item => {
        return Date.parse(this.startDate) < Date.parse(item.date.toString()) || Date.parse(this.endDate) > Date.parse(item.date.toString());
      });
      let condition = null;
      this.startDate || this.endDate ? condition = filterDate : condition = this.documentList;
      this.listLength = condition.length;
      this.setPages();
      return this.paginate(condition);
    }
  }
}
</script>