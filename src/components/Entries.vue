<template>
  <div>
    <button @click="otherWay">Newest to oldest</button>
    <div class="post" v-for="post in sortedEntries" :key="post.id">
      <h3>{{ post.title }}</h3>
      <p>{{ post.date | date(post.date) }}</p>
      <img :src="post.image">
      <p>{{ post.text }}</p>
    </div>
  </div>
</template>

<script>
import moment from 'moment';
export default {
  name: 'Entries',
  props: {
    entries: Array
  },
  computed: {
    sortedEntries: function () {
      let a = this.entries
      return a.sort((a, b) => new Date(a.date) - new Date(b.date)).reverse()
    }
  },
  filters:{
    date: function (newDate){
      return moment(String(newDate)).format("dddd, MMMM, Do YYYY, h:mm a")
    }
  },
  methods:{
    otherWay: function (){
      this.entries.reverse()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
