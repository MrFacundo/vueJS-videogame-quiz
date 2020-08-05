<template>
	<div class="questions-container">
		<b-jumbotron>
			<template v-slot:lead>
				{{ currentQuestion.question}}
			</template>

			<hr class="my-4">

			<b-list-group>
				<b-list-group-item
					v-for="(answer, index) in answers" 
					:key="index"
					@click.prevent="selectAnswer(index)"
					:class="answerClass(index)"
					>
						{{ answer }}
				</b-list-group-item>
			</b-list-group>

			<div class="box-button">
				<b-button variant="primary"
				@click="submitAnswer"
				:disabled="selectedIndex === null || answered"
				>Submit</b-button>

				<b-button variant="success"
				@click="next"
				:disabled="answered === false"
				>Next</b-button>
			</div>

		</b-jumbotron>
	</div>
</template>

<script>
	import _ from 'lodash'
	export default {
		props: {
			currentQuestion: Object,
			next: Function,
			increment: Function
		},
		data() {
			return {
				selectedIndex: null,
				correctIndex: null,
				shuffledAnswers: [],
				answered: false
			}
		},
		computed: {
			answers() {
				let answers = [...this.currentQuestion.incorrect_answers]
				answers.push(this.currentQuestion.correct_answer)
				return answers
			}
		},
		watch: {
			currentQuestion: {
				immediate: true,
				handler() {
					this.selectedIndex = null
					this.answered = false
					this.shuffleAnswers()	  
				}
			}
		},
		methods: {
			selectAnswer(index) {
				this.selectedIndex = index
			},
			submitAnswer() {
				let isCorrect = false
				if (this.selectedIndex === this.correctIndex) {
					isCorrect = true
				}
				this.answered = true

				this.increment(isCorrect)
			},
				shuffleAnswers() {
					let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
					this.shuffledAnswers = _.shuffle(answers)
					this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
			},
			answerClass(index) {
				let answerClass = ''

				if (!this.answered && this.selectedIndex === index) {
					answerClass = 'selected'
				} else if (this.answered && this.correctIndex === index) {
					answerClass = 'correct'
				} else if (this.answered && this.selectedIndex === index && this.correctIndex !== index) {
					answerClass = 'incorrect'
				}
				return answerClass
			}
		}
	}
</script>

<style scoped>
	.list-group {
		margin-bottom: 15px;
		border-radius: 15px;

	}

	.list-group-item {
		margin-top: 15px;
		border-radius: 15px;
	}

	.list-group-item:hover {
		background: #eeeeee;
		cursor: pointer;
	}
	.box-button {
		display: flex;
		width: 100%;
	}

	.box-button button{
		width: 150px;
		height: 35px;
		margin: auto;
		margin-top: 30px;
	}
	.btn {
		margin: 0 5px;
	}

	.selected {
		background-color: lightblue;
	}

	.correct {
		background-color: lightgreen;
	}

	.incorrect {
		background-color: orangered;
	}

	.questions-container {
		padding-top: 50px;
	}

</style>

<style >

	.jumbotron {
		box-shadow: 0 10px 20px rgba(0, 0, 0, 0.19), 0 6px 6px rgba(0, 0, 0, 0.19);
	}

</style>