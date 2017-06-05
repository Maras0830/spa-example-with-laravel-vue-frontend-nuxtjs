<template>
  <section class="container">
    <header/>
    <div class="content">
      <logo/>
      <h1 class="title ">
        Posts List
      </h1>
      <ul>
        <li v-for="post in posts">
          <article>
            <nuxt-link :to="{ name: 'posts-id', params: { id: post.id } }">{{ post.title }}</nuxt-link>
            <span> By <nuxt-link :to="{ name: 'authors-id', params: { id: post.author.data.id } }">{{ post.author.data.name }}</nuxt-link></span>
            <span> - {{ post.time_ago }}</span>
            <span><icon class="icon-comment" name="comment"></icon> {{ post.comments.data.length }} reply</span>
          </article>
        </li>
        <div class="links">
        <router-link to="/posts" class="button--green">< Home</router-link>
        <router-link :to="{ name: 'authors' }" class="button--green">Authors</router-link>
        </div>
      </ul>
    </div>
  </section>
</template>

<script>
import Header from '~components/Header.vue'
import Logo from '~components/Logo.vue'
import axios from 'axios'

export default {
  components: {
    Header,
    Logo
  },
  asyncData ({ req, params }) {
    return axios.get(process.env.baseURL + `/posts`)
    .then((res) => {
      return { posts: res.data.data }
    })
  }
}
</script>

<style>
.container
{
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  width: 100%;
}
.content
{
  width: 100%;
}
.title
{
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}
.icon-comment
{
  margin-left: 1em;
}
ul
{
  list-style: none;
}
li
{
  padding: 10px;
}
.links
{
  padding-top: 15px;
}
</style>
