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
      let url = 'https://content.guardianapis.com/search?api-key=f192c3df-0d0f-43ff-8683-930af2d73fbd';
      let req = new Request(url);
      fetch(req)
              .then(response => response.json())
              .then((data) => {
// eslint-disable-next-line no-console
                console.log(data);
                let dataParse = [];
// eslint-disable-next-line no-console
                for (let i = 0; i < data.response.results.length; i++) {
// eslint-disable-next-line no-console
                  console.log("sasdasd" ,data.response.results);
                  let obj = {
                    title: "",
                    url: ""
                  };
                  obj.title = data.response.results[i].webTitle;
                  obj.url = data.response.results[i].webUrl;
                  dataParse.push(obj)
                }
// eslint-disable-next-line no-console
                console.log("Data is parse: ", dataParse);
                this.obj = dataParse
              });
      return {
        obj: {},
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