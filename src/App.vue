<template>
	<div id="app">
		<h1>Super Quiz</h1>
		<Question
			v-if="questionMode"
			:questions="questions[currentQuestion]"
			@response="showResult"
		/>
		<Result
			v-else
			:result="result"
			@nextQuestion="next"
		/>
	</div>
</template>

<script>
import Result from './components/Result.vue'
import questions from './util/questions'
import Question from './components/Question.vue'

export default {
	components: {Result, Question},
	data () {
		return {
			result: true,
			questionMode: true,
			questions,
			currentQuestion: 0,
			questionResponse: []
		}
	}, 
	methods: {
		showResult(value){
			this.questionMode = false
			this.result = value
		},	
		next(value){
			if(value){
				this.currentQuestion = this.getRandom(questions.length)
				this.questionResponse.push(this.currentQuestion)
				this.questionMode = true
			}
		},
		getRandom(max){
			return Math.floor(Math.random() * max)
		}
	}
}
</script>

<style>
body {
	background: linear-gradient(to right, rgb(0, 0, 70), rgb(28, 181, 224));
	font-family: 'Oswald', sans-serif;
	color: #FFF;
	height: 100vh;
}

#app {
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;

	display: flex;
	flex-direction: column;
	align-items: center;
}

#app h1 {
	font-weight: 200;
	font-size: 4rem;
}

@keyframes flip-out {
	from { transform: rotateY(0deg); }
	to { transform: rotateY(90deg); }
}

@keyframes flip-in {
	from { transform: rotateY(90deg); }
	to { transform: rotateY(0deg); }
}

.flip-enter-active {
	animation: flip-in 0.3s ease;
}

.flip-leave-active {
	animation: flip-out 0.3s ease;
}
</style>
