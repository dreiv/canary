<script setup lang="ts">
import news from './assets/data.json'

function formatDate(dateString: string) {
  const date = new Date(dateString)
  return date.toLocaleDateString(undefined, {
    year: 'numeric',
    month: 'long',
    day: 'numeric',
    hour: 'numeric',
    minute: 'numeric',
  })
}
</script>

<template>
  <div class="news-container">
    <h1>Top News</h1>
    <div v-if="news.length === 0">Loading...</div>
    <div v-else class="news-list">
      <div v-for="article in news" :key="article.url" class="news-item">
        <a :href="article.url" target="_blank" class="news-link">
          <div class="news-image" v-if="article.urlToImage">
            <img :src="article.urlToImage" alt="Article Image" />
          </div>
          <div class="news-content">
            <h2>{{ article.title }}</h2>
            <p v-if="article.description">{{ article.description }}</p>
            <div class="news-meta">
              <span v-if="article.author">Author: {{ article.author }}</span>
              <span v-if="article.source && article.source.name"
                >Source: {{ article.source.name }}</span
              >
              <span>{{ formatDate(article.publishedAt) }}</span>
            </div>
          </div>
        </a>
      </div>
    </div>
  </div>
</template>

<style scoped>
.news-container {
  max-width: 800px;
  margin: 20px auto;
  padding: 20px;
  font-family: sans-serif;
}

.news-list {
  display: grid;
  grid-gap: 20px;
}

.news-item {
  border: 1px solid #ddd;
  border-radius: 8px;
  overflow: hidden;
  transition:
    transform 0.2s ease-in-out,
    box-shadow 0.2s ease-in-out;
}

.news-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.news-link {
  display: flex;
  text-decoration: none;
  color: inherit;
}

.news-image {
  flex: 0 0 200px;
  overflow: hidden;
}

.news-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.news-content {
  flex: 1;
  padding: 15px;
}

.news-content h2 {
  margin-top: 0;
  font-size: 1.2em;
  margin-bottom: 5px;
}

.news-content p {
  margin-bottom: 10px;
  line-height: 1.5;
}

.news-meta {
  font-size: 0.9em;
  color: #888;
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}
</style>
