<template>
    <div class="results-container">
        <b-jumbotron>
            <h1>Your score is</h1>
            <h2>{{ numCorrect }}/{{ numTotal }}</h2>
            <b-button variant="primary"
						@click="nextQuiz">Try again</b-button>
        </b-jumbotron>
    </div>

</template>>

<script>
export default {
	props: {
		nextQuiz: Function,
		numCorrect: Object,
		numTotal: Object	
	}
}
</script>>

<style scoped>

  .results-container {
		padding-top: 50px;
	}

</style>