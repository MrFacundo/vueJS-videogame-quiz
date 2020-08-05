<template>
	<div pb-3>
		<b-nav tabs>
				<b-nav-item disabled><b>Videogames quiz</b></b-nav-item>
				<b-nav-item disabled>Question {{ index + 1 }}/10 </b-nav-item>
		</b-nav >
		<div class='nav-container'>
			<div class="step-progress-bar"><div class="step-progress" :style="{'width': progress + '%'}"></div></div>
		</div >

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
	.step-progress-bar {
		display: flex;
		margin: 20px;
		width: 40%;
		background-color:red;
		border: 5px solid black;
		border-radius: 5px;
		transform: skewX(-10deg);
		transition: 0.5s;
	}
	.nav-tabs {
		align-items: center;
		justify-content: center;
	}

	.nav-container {
		display: flex;
		justify-content: center;
	}

	.step-progress {
		display: flex;
		width: 20%;
		height: 25px;
		background-color: #A1DD00;
		transition: 0.5s;
	}
</style>