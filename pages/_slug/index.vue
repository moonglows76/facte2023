<template>
  <main class="main">
    <NuxtLink to="/">TOPに戻る</NuxtLink>

    <!-- タイトル -->
    <h1 class="title">
      {{ title }}
    </h1>

    <!-- 排気量（入っていれば表示） -->
    <div
      v-if="bike_scorecc.length > 0"
      class="bike_scorecc"
    >
      排気量：{{ bike_scorecc[0] }}
    </div>

    <!-- 車種（入っていれば表示） -->
    <div
      v-if="car_type.length > 0"
      class="car_type"
    >
      車種：{{ car_type[0] }}
    </div>

    <!-- 画像 -->
    <div class="icon">
      <img :src="icons.url" alt="">
    </div>

  </main>
</template>

<script>
export default {
  // $microcms は nuxt.jsからmicrocmsを便利に使うためのプログラム
  // nuxt-microcms-module をインストール（npm install nuxt-microcms-module）して、
  // nuxt.config.jsにいくらか書き込むと利用できるようになる
  // 参考：nuxt-microcms-moduleの初期化
  // https://document.microcms.io/tutorial/nuxt/nuxt-getting-started#hb78937a099
  // paramsはnuxt.jsの機能で、URL情報を見ることができるオブジェクト
  async asyncData({ $microcms, params }) {
    // axiosの代わりに$microcmsを使う

    // `` はテンプレートリテラルで文字とスクリプトを一緒に書くことができる特殊な引用符
    // ${params.slug} はURLにある http://localhost:3000/suzuki-sv-650x-abs の suzuki-sv-650x-abs を取得
    // slugという名前は pages/_slug/index.vue とフォルダ名をつけているから、そのように指定する

    // pages/bike/_bikeId/index.vue だったら、
    // http://localhost:3000/bike/suzuki-sv-650x-abs でアクセスできて、
    // ${params.bikeId} で suzuki-sv-650x-abs を取得
    const data = await $microcms.get({
      endpoint: `facte/${params.slug}`,
    });
    return data;
  },
}
</script>
