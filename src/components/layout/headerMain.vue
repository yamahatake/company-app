<template>
  <header class="negative">
    <picture>
      <img src="../../assets/images/logo.png"/>
    </picture>
    <div id="userLogin">
      <picture>
        <img src="../../assets/images/icon-user.png"/>
      </picture>
      <p>Augusto Yamamoto</p>
    </div>
    <nav id="mainNav">
      <a>Home</a>
      <a class="selected">Documents</a>
      <a>Contacts</a>
    </nav>
  </header>
</template>

<script>
export default {
  name: 'headerMain'
}
</script>