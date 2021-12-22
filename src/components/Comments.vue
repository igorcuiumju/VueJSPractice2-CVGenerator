<template>
	<div v-if="commentsData.length != 0" class="card">
      <h2>Комментарии</h2>
      <ul class="list">
        <li 
          v-for="comment in commentsData"
          :key="comment.id" 
          class="list-item"
        >
          <div>
            <p><strong>{{comment.email}}</strong></p>
            <small>{{comment.body}}</small>
          </div>
        </li>
      </ul>
    </div>
</template>


<script>
export default {
	name: 'Comments',
	props: {
		commentsData: Object
	}
}
</script>