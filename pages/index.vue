<template>
  <div class="container bg-gray-200 min-h-screen p-2">
    <div class="grid grid-cols-4 gap-3 bg-gray-50 p-2">
      <ul class="bg-purple-100 p-4 rounded-lg shadow-md" v-for="headline in headlines" :key="headline.title">
        <card class="flex flex-col justify-center items-center text-gray-600 mt-1 rounded-md">
          <img :src="headline.urlToImage" :alt="headline.title">
          <a class="text-base font-medium tracking-tight text-gray-600 mt-2 hover:text-red-800" :href="headline.url">{{headline.title}}</a>
          <div class="text-sm flex-none justify-end text-red-400">
            Source: {{headline.source.name}}
          </div>
        </card>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ app }){
    const topHeadlines =  await app.$axios.$get('/api/top-headlines?country=us');
    return { headlines: topHeadlines.articles }
  }
}
</script>