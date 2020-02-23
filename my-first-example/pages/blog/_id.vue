<template>
  <div class="container">
    <div class="card">
      <div class="card-bod">
        <h1>{{ posts.title }}</h1>
        <p class="small">{{ posts.nameUser }}</p>
        <p>{{ posts.body }}</p>
        <nuxt-link to="/blog" class="btn btn-primary">Atrás</nuxt-link>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {};
  },
  // async created() {},
  async asyncData({
    isDev,
    route,
    store,
    env,
    params,
    query,
    req,
    res,
    redirect,
    error
  }) {
    try {
      const res = await axios.get(
        `https://jsonplaceholder.typicode.com/posts/${params.id}`
      );
      const posts = res.data;
      const resUser = await axios.get(
        `https://jsonplaceholder.typicode.com/users/${res.data.userId}`
      );
      posts.nameUser = resUser.data.name;
      // console.log(resUser.data);
      return { posts };
    } catch (error) {
      console.log("TCL: created -> error", error);
      return { error: error };
    }
  }
};
</script>
