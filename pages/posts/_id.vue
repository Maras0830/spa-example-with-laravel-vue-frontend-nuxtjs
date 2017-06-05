<template>
  <section class="container">
    <header/>
    <div>
      <logo/>
      <h2 class="title ">
        {{ post.title }}
      </h2>
      <h3>
          By <nuxt-link :to="{ name: 'authors-id', params: { id: post.author.data.id } }">{{ post.author.data.name }}</nuxt-link> - {{ post.time_ago }}
      </h3>
      <div class="content">
        {{ post.content }}
      </div>
      <router-link to="/posts">Go to my Posts Page</router-link>
      <ul class="reply">
          <div>
            <span><icon class="icon-comment" name="comment"></icon>{{ post.comments.data.length }} reply</span>
            <ul v-for="comment in post.comments.data">
              <li>{{ comment.title }}</li>
              <li>{{ comment.content }}</li>
              <li></li>
              <li>By <nuxt-link :to="{ name: 'authors-id', params: { id: comment.author.data.id } }">{{ comment.author.data.name }}</nuxt-link> - {{ comment.time_ago }}</li>
            </ul>
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
    return axios.get(process.env.baseURL + `/posts/${params.id}`)
    .then((res) => {
      return { post: res.data.data }
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
.content
{
  margin: 3em;
}
.reply
{
  margin: 3em;
  background: #DDDDDD;
  min-height: 300px;
}
</style>
