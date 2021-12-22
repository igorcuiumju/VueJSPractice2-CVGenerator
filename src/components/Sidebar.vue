<template>
	<form class="card card-w30">
		<div class="form-control">
			<label for="type">Тип блока</label>
			<select id="type" v-model="type">
				<option value="title">Заголовок</option>
				<option value="subtitle">Подзаголовок</option>
				<option value="avatar">Аватар</option>
				<option value="text">Текст</option>
			</select>
		</div>

		<div class="form-control">
			<label for="value">Значение</label>
			<textarea v-model="textVal" id="value" rows="3"></textarea>
		</div>

		<button 
			@click.prevent="sendVal(type, textVal)" 
			:disabled="disabledBtn"
			class="btn primary" 
		>Добавить</button>
	</form>
</template>

<script>
export default {
	name: 'Sidebar',
	data() {
		return {
			type: 'title',
			textVal: '',
			disabled: true
		}
	},
	emits: ['cv-textVal'],
	methods: {
		sendVal(textVal, type) {
			this.$emit('cv-textVal', type, textVal)
			this.textVal = ''
			this.type =  'title'
		}
	},
	computed: {
		disabledBtn() {
			return this.disabled ? this.textVal.length < 4 : '';
		}
	}

}
</script>