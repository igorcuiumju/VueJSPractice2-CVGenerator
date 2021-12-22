<template>
  <div class="container column">
    
    <sidebar @cv-textVal="contentVal"></sidebar>
    
    <cv-layout>
      <div 
        v-for="(data, idx) in textboxValue"
        :key="idx"
      >
        <div v-html="data"></div>
      </div>
    </cv-layout>

  </div>

  <div class="container">
    <p v-if="commentsData.length === 0">
      <button @click="getComments" class="btn primary">Загрузить комментарии</button>
    </p>
    
    <comments
      :commentsData="commentsData"
    ></comments>

    <div v-if="loader" class="loader"></div>
  </div>

</template>

<script>
 import Sidebar from "../src/components/Sidebar.vue"
 import CVLayout from "../src/components/CVLayout.vue"
 import Comments from "../src/components/Comments.vue"

export default {
  data() {
    return {
      textboxValue: [],
      commentsData: [],
      loader: false
    }
  },
  components: {
    'sidebar': Sidebar,
    'cv-layout': CVLayout,
    'comments': Comments
  },
  methods: {
    contentVal(textVal, type) {
      if(type === 'title') {
        this.textboxValue.push(`<h1>${textVal}</h1>`)
      } else if(type === 'subtitle') {
        this.textboxValue.push(`<h2>${textVal}</h2>`)
      } else if(type === 'avatar') {
        this.textboxValue.push(`
          <div class="avatar">
            <img src="${textVal}"/>
          </div>
        `)
      } else {
        this.textboxValue.push(`<p>${textVal}</p>`)
      }
    },
    async getComments() {
      this.loader = true
      await fetch("https://jsonplaceholder.typicode.com/comments?_limit=42")
        .then(response => response.json())
        .then(data => ( this.commentsData = data));
      this.loader = false
     }
  },
}
</script>

<style>
  .avatar {
    display: flex;
    justify-content: center;
  }

  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }
</style>

