<template>
	<div pb-3>
		<b-nav tabs>
				<b-nav-item disabled><b>Quiz</b></b-nav-item>
				<b-nav-item disabled>Question {{ index + 1 }}/10 </b-nav-item>
		</b-nav >
		<div class="step-progress" :style="{'width': progress + '%'}"></div>

	</div>
</template>

<script>
export default {
	props: [
		'index',
		'progress'
	]
	
}
</script>

<style>
	.step-progress {
		display: flex;
		margin: 20px;
		width: 40%;
		height: 25px;
		background-color: #A1DD00;
		border: 5px solid black;
		border-radius: 5px;
		transform: skewX(-10deg);
		transition: 0.5s;
	}
</style>