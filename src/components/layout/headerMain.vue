<template>
  <header class="negative">
    <picture>
      <img src="../../assets/images/logo.svg"/>
    </picture>
    <div id="menu" :class="{'active':mobileMenu}">
      <nav id="mainNav">
        <a>Home</a>
        <a class="selected">Documents</a>
        <a>Contacts</a>
      </nav>
      <div id="userLogin">
        <picture>
          <img src="../../assets/images/icon-user.png"/>
        </picture>
        <p>{{user.firstName}}<br>{{user.lastName}}</p>
      </div>
    </div>
    <a class="menuToggle" :class="{'close':mobileMenu}" @click="toggleMenu()"></a>
  </header>
</template>

<script>
import axios from 'axios';
export default {
  name: 'headerMain',
  data(){
    return {
      user: [],
      mobileMenu: false
    }
  },
  methods: {
    toggleMenu(){
      this.mobileMenu = !this.mobileMenu;
    }
  },
  created() {
    const proxyUrl = 'https://cors-anywhere.herokuapp.com/';
    axios.get(`${proxyUrl}https://apply.crosslend.io/user/info`)
    .then(response => {
      this.user = response.data.body.User.profile;
    })
  }
}
</script>