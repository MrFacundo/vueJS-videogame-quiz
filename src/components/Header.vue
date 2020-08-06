<template>
	<div pb-3>
		<b-nav tabs>
				<b-nav-item disabled><b>Quiz</b></b-nav-item>
				<b-nav-item disabled>Question {{ index + 1 }}/10 </b-nav-item>
		</b-nav >
	</div>
</template>

<script>
export default {
	props: [
		'index'
	]
}
</script>>