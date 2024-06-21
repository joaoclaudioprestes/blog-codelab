<script setup>
import { ref } from "vue";
import { Search } from "lucide-vue-next";
import postsData from "./mock/posts.json";
import PostBlog from "./components/PostBlog.vue";
import "./assets/base.css";

const posts = ref(postsData.posts);

const filterPosts = (event) => {
  const search = event.target.value.toLowerCase();
  const filteredPosts = postsData.posts.filter((post) => {
    return post.title.toLowerCase().includes(search) || post.description.toLowerCase().includes(search);
  });

  if (filteredPosts.length === 0) {
    posts.value = [{ date: "", title: "Post não encontrado!", description: "Tente buscar por outras palavras chaves..." }];
  } else {
    posts.value = filteredPosts;
  }
}

</script>

<template>
  <header>
    <h1>Code<span>Lab</span></h1>
    <label for="inpSearch">
      <Search class="icon-search" />
      <input type="text" name="input-blog-search" id="inpSearch" placeholder="Pesquisar no Blog" @input="filterPosts" />
    </label>
  </header>

  <main>
    <PostBlog v-for="post in posts" :key="post.id" :date="post.date" :title="post.title"
      :description="post.description" />
  </main>

  <footer>
    <p>
      © 2024 -
      <a href="https://github.com/iuricode/desafios-frontend" target="_blank">CodeLab</a>
      Challenges - Solved by
    </p>
    <a href="https://jprestes.vercel.app" target="_blank"><img src="/public/logo.svg" alt="Logo - João Prestes"
        class="logo" /></a>
  </footer>
</template>


<style scoped>
header {
  background-color: var(--dark-20);
  padding: 4.4rem 0;
  display: flex;
  flex-direction: column;
  gap: 4.4rem;
  align-items: center;
  justify-content: center;
}

h1 {
  font-size: 4rem;
  color: var(--brand-color);
  font-family: var(--font_space_grotesk);
  font-weight: 500;

  & span {
    color: var(--white);
  }
}

label {
  display: flex;
  align-items: center;

  & .icon-search {
    position: absolute;
    margin-left: 2rem;
    color: var(--brand-color);
  }

  & input {
    width: 750px;
    height: 4.4rem;
    border-radius: 8px;
    outline: none;
    padding: 0.4rem;
    background-color: var(--dark-30);
    border: 2px solid var(--dark-40);
    color: var(--white);
    font-size: 1.6rem;
    font-family: var(--font_inter);
    padding: 1.6rem 0 1.6rem 5.6rem;
  }
}

main {
  padding-top: 40px;
  padding-bottom: 40px;
  display: flex;
  flex-direction: column;
  align-items: center;
  height: auto;
  display: flex;
  flex-direction: column;
  gap: 40px;
}

footer {
  background-color: var(--dark-20);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.4rem;
  color: var(--white);
  font-family: var(--font_inter);
  padding: 1.5rem;
  text-align: center;
  position: static;
  bottom: 0;
  width: 100%;

  & a {
    color: #ffa500;
    font-weight: 500;
  }
}

.logo {
  width: 3rem;
  height: 3rem;
  margin-left: 4px;
  cursor: pointer;
}

@media (max-width: 768px) {
  label {
    width: 90%;

    & input {
      width: 100%;
    }
  }
}
</style>
