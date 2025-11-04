<template>

  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://fonts.googleapis.com/css2?family=Pacifico&display=swap" rel="stylesheet">
  </head>

  <body>
    <h1 :class="title">标题<img src="C:\Users\LiJunde\OneDrive\画像\google_logo.svg" alt=""></h1>
    <SearchBox />
    <table class="shortcut">
      <tbody>
        <tr class="short">
          <td class="cut"><a href="https://www.bilibili.com/"><img width="15%" src="@/assets/bilibili.ico" alt=""></a>
          </td>
          <td class="cut"></td>

  
          <td class="cut"></td>
          <td class="cut"></td>
          <td class="cut"></td>
          <td class="cut"></td>
        </tr>
      </tbody>
    </table>
  </body>

</template>

<style>
@import'@/assets/HomePage.css';
</style>

<script>
import SearchBox from './SearchBox.vue';

export default {
  name: 'HomePage',

  components: {
    SearchBox
  },

  props: {
    msg: String
  },

  data() {
    return {
      title: "title",
    }
  },

  methods: {
  }

}
</script>
