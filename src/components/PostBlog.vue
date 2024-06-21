<script setup>
import { Heart } from "lucide-vue-next";
import { ref, defineProps } from "vue";

defineProps({
  id: String,
  date: String,
  title: String,
  description: String,
});

let isFavorite = ref(false);

const toggleFavorite = () => {
  isFavorite.value = !isFavorite.value;
};
</script>

<template>
  <div :key="id" class="card" :class="{ cardfavorit: isFavorite }" @click="toggleFavorite">
    <div class="icon-div">
      <span>{{ date }}</span>
      <button>
        <Heart :class="{ favorit: isFavorite }" />
      </button>
    </div>
    <h3>{{ title }}</h3>
    <p>{{ description }}</p>
  </div>
</template>

<style scoped>
.card {
  background-color: var(--dark-20);
  width: 750px;
  padding: 4rem;
  display: flex;
  flex-direction: column;
  border: 2px solid var(--dark-40);
  border-radius: 8px;
  cursor: pointer;
  gap: 16px;
  transition: border-color 0.5s ease-in-out;

  & span {
    color: var(--brand-color);
    font-family: var(--font_inter);
    font-weight: 500;
    font-size: 1.3rem;
    margin-bottom: 4px;
  }

  & h3 {
    color: var(--white);
    font-family: var(--font_space_grotesk);
    font-weight: 500;
    font-size: 1.9rem;
  }

  & p {
    color: var(--gray);
    font-family: var(--font_space_grotesk);
    font-weight: 500;
    font-size: 1.4rem;
  }

  & .icon-div {
    display: flex;
    justify-content: space-between;
    align-items: center;

    & button {
      background-color: transparent;
      border: none;
      cursor: pointer;
      outline: none;
      color: var(--brand-color);
    }
  }

  &:hover {
    border-color: var(--brand-color);
  }
}

.favorit {
  fill: var(--brand-color);
}

.cardfavorit {
  border-color: var(--brand-color);
}

@media (max-width: 768px) {
  .card {
    max-width: 90%;
    padding: 2rem;
  }
}
</style>
