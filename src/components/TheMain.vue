<template>
  <div class="row row-cols-5 g-3">
    <template v-if="musicList">
      <div class="col" v-for="(album, i) in musicList" :key="i">
        <div class="p-2 text-center my-card h-100">
          <div>
            <img :src="album.poster" alt="">
          </div>
          <h5 class="pt-4 text-white text-uppercase">{{ album.title }}</h5>
          <div class="text-muted mt-4">{{ album.author }}</div>
          <div class="text-muted">{{ album.year }}</div>
        </div>
      </div>
    </template>
  </div>
</template>

<script>


export default {
  name: 'TheMain',
  props: {
    musicList: Array
  }
}
</script>


<style scoped lang="scss">
  img {
    width: 100%;
  }

  .my-card {
    background-color: #2D3B46;
  }
</style>
