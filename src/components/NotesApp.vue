<script>
export default {
	data() {
		return {
			newNote: {
                title: '',
				category: 'Без категории',
				text: ''
            },
			notes: [
				{title: 'Название', category: 'Без категории', text: 'Содержание заметки'},
				{title: 'Название', category: 'Учёба', text: 'Содержание заметки'},
				{title: 'Название', category: 'Важное', text: 'Содержание заметки'}
			],
		};
	},
	methods: {
		add() {
			if(!this.newNote.title || !this.newNote.text) {
				return
			}
			this.notes.push({...this.newNote})
            this.newNote.title = ''
			this.newNote.category = 'Без категории'
			this.newNote.text = ''
		}
	}
};

</script>


<template>
	<div class="notes-app container">
		<div class="row row-cols-2 g-3 mt-3">
			<!-- Форма -->
			<div class="col notes-app-form">
				<div class="form-floating">
					<input type="text" class="form-control" id="title" v-model="newNote.title" />
					<label for="title">Название</label>
				</div>
				<div class="form-floating my-3">
					<select class="form-select" id="category" v-model="newNote.category">
						<option value="Без категории">Без категории</option>
						<option value="Важное">Важное</option>
						<option value="Учёба">Учёба</option>
					</select>
					<label for="category">Категория</label>
				</div>
				<textarea
					class="form-control my-3"
					rows="5"
					id="text"
					placeholder="Введите текст"
					v-model="newNote.text"
				></textarea>
				<div class="btn-group d-flex justify-content-center my-3">
					<button type="button" class="btn btn-outline-secondary" @click="add">
						Сохранить
					</button>
				</div>
			</div>
			<!-- Заметки -->
			<div class="col notes">
				<div v-for="(item, index) in notes" :key="index" class="row row-cols-2 notes-container">
					<div class="col">
						<div class="card">
							<div class="card-body" :class="{
							study: item.category === 'Учёба',
							important: item.category === 'Важное'}">
								<h5 class="card-title">{{ item.title }}</h5>
								<h6 class="card-subtitle mb-2 text-muted">{{ item.category }}</h6>
								<p class="card-text">{{ item.text }}</p>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<style>
.important {
	background-color: rgba(224, 105, 240, 0.664);
}

.study {
	background-color: rgb(140, 240, 140);
}

.notes-app {
	max-width: 1000px;
}
.col.notes-app-form {
	margin-top: 20px;
}
.notes {
	display: flex;
	flex-direction: column;
	gap: 30px;
	flex-wrap: wrap;
}
.notes-container {
	width: 900px;
	display: flex;
	flex-wrap: wrap;
}
</style>
