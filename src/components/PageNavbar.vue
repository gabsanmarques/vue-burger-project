<template>
  <nav id="page-nav">
    <router-link to="/" id="logo-url">
      <img :src="logo" :alt="alt" id="logo" />
    </router-link>
    <router-link to="/">Home</router-link>
    <router-link to="/orders">Orders</router-link>
  </nav>
</template>

<script lang="ts">
export default {
  name: "PageNavbar",
  props: {
    logo: {
      type: String,
      required: true,
    },
    alt: {
      type: String,
      required: true,
    },
  },
};
</script>

<style scoped>
#page-nav {
  display: flex;
  background-color: #222;
  padding: 15px 50px;
  align-items: center;
  justify-content: flex-end;
  gap: 20px;
}

#logo-url {
  margin: auto;
  margin-left: 0;
}

#logo {
  width: 40px;
}

#page-nav a {
  color: #fcba73;
  text-decoration: none;
  transition: 0.5s;
}

#page-nav a:hover {
  color: #fff;
}
</style>
