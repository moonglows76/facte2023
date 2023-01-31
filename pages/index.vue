<template>
  <div>
    <h1>facte</h1>

    <!--  -->
    <h2>すべての一覧</h2>
    <ul>
      <li v-for="content in contents" :key="content.id">
        <nuxt-link :to="`/${content.id}`">
          {{ content.title }}
        </nuxt-link>
      </li>
    </ul>

    <!--  -->
    <h2>250ccのバイク一覧</h2>
    <ul>
      <li v-for="bike in Bikes250cc" :key="bike.id">
        <NuxtLink :to="`${bike.id}`">
          {{ bike.title }}
        </NuxtLink>
      </li>
    </ul>

    <!--  -->
    <h2>400ccのバイク一覧</h2>
    <ul>
      <li v-for="bike in Bikes400cc" :key="bike.id">
        <NuxtLink :to="`${bike.id}`">
          {{ bike.title }}
        </NuxtLink>
      </li>
    </ul>

    <!--  -->
    <h2>400cc overのバイク一覧</h2>
    <ul>
      <li v-for="bike in Bikes400ccover" :key="bike.id">
        <NuxtLink :to="`${bike.id}`">
          {{ bike.title }}
        </NuxtLink>
      </li>
    </ul>

  </div>
</template>

<script>
export default {
  // $microcms は nuxt.jsからmicrocmsを便利に使うためのプログラム
  // nuxt-microcms-module をインストール（npm install nuxt-microcms-module）して、
  // nuxt.config.jsにいくらか書き込むと利用できるようになる
  // 参考：nuxt-microcms-moduleの初期化
  // https://document.microcms.io/tutorial/nuxt/nuxt-getting-started#hb78937a099
  async asyncData({ $microcms }) {
    // axiosの代わりに$microcmsを使う（先生の環境ではなぜかaxiosが動かなかったので、$microcmsを使いました）
    //
    const data = await $microcms.get({
      endpoint: 'facte',
      queries: { limit: 100 }
    });
    return data;
  },
  computed: {
    Bikes250cc() {
      return this.contents.filter(el => el.bike_scorecc[0] === '250cc')
    },
    Bikes400cc() {
      const bikes = this.contents.filter(el => el.bike_scorecc[0] === '400cc')
      return bikes
    },
    Bikes400ccover() {
      const bikes = this.contents.filter(el => el.bike_scorecc[0] === '400ccover')
      return bikes
    },
  },
}
</script>
