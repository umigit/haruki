<template>
  <header>
    <div class="header-content">
      <h1 class="title">Haruki's Room</h1>
      <div class="links">
        <nuxt-link to="/">HOME</nuxt-link>
        <nuxt-link to="/profile">PROFILE</nuxt-link>
        <nuxt-link to="/books">BOOKS</nuxt-link>
      </div>
    </div>
  </header>
</template>

<style>
header {
  background-color: transparents;
  width: 100%;
  height: 80px;
  position: fixed;
  top: 0;
}

.header-content {
  width: 1020px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 0 auto;
}

h1 {
  color: white;
  font-size: 50px;
  padding: 10px 20px;
}

.links {
  margin-right: 30px;
}
.links > a{
  color: white;
  font-size: 25px;
  font-weight: bold;
  text-decoration: none;
  padding: 5px 10px;
}
</style>

