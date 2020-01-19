<template>
  <div id="app">
    <h1>News</h1>
    <List v-bind:obj="obj"> </List>
  </div>
</template>

<script>
  import List from "@/components/List";
  export default {
    name: 'app',
    data() {
      return {
        obj: [],
        i: this.mounted()
      }
    },
    methods: {
      mounted() {
        let url = 'https://newsapi.org/v2/top-headlines?' +
                'country=us&' +
                'apiKey=ef295b674d2e48fcb3eeb97c6b3eb3c4';
        let req = new Request(url);
        fetch(req)
                .then(response => response.json())
                .then((data) => {
                  let dataParse = [];
                  // eslint-disable-next-line no-console
                  for (let i = 0; i < data.articles.length; i++) {
                    // eslint-disable-next-line no-console
                    let obj = {
                      title: "",
                      url: ""
                    };
                    obj.title = data.articles[i].title;
                    obj.url = data.articles[i].url;
                    dataParse.push(obj)
                  }
                  // eslint-disable-next-line no-console
                  console.log("Data is parse: ", dataParse);
                  this.obj = dataParse
                });
      }
    },
    components: {
      List
    }
  }
  //
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>