<script>
import { onMounted } from 'vue';

export default {
	data() {
		return {
			questions: [
				{
					question: 'Что такое Vue?',
					right: 0,
					answers: [
						'Фреймворк',
						'Библиотека',
						'Архитектура'
					]
				},
				{
					question: 'Какой архитектурой вдохновлен Vue?',
					right: 1,
					answers: [
						'MVC',
						'MVVM',
						'FSD'
					]
				},
				{
					question: 'Какой подход во Vue?',
					right: 2,
					answers: [
						'Императивный',
						'Интуитивный',
						'Декларативный'
					]
				},
				{
					question: 'Какой синтаксис используется для объявления компонентов в Vue?',
					right: 2,
					answers: [
						'JSX',
						'HTML',
						'Vue-шаблон'
					]
				},
				{
					question: 'Что такое директивы во Vue?',
					right: 0,
					answers: [
						'Специальные атрибуты',
						'Компоненты',
						'Фильтры'
					]
				},
				{
					question: 'Какая директива используется для обработки событий в Vue?',
					right: 1,
					answers: [
						'v-model',
						'v-on',
						'v-if'
					]
				},
				{
					question: 'Какой хук используется для выполения кода после рендеринга компонента?',
					right: 2,
					answers: [
						'onCreate',
						'onRender',
						'onMounted'
					]
				},
				{
					question: 'Какой метод следует использовать для отправки HTTP-запросов в Vue?',
					right: 0,
					answers: [
						'Методы компонента',
						'Вычисляемые свойства',
						'Хуки'
					]
				},
				{
					question: 'Какой метод используется для реактивного изменения значения переменной в Vue?',
					right: 1,
					answers: [
						'setData',
						'reactive',
						'updateValue'
					]
				},
				{
					question: 'Какой пакет следует использовать для маршрутизации в Vue?',
					right: 2,
					answers: [
						'vue-router',
						'vue-route',
						'vue-navigation'
					]
				}
			],
			currentQuestion: 0,
			score: 0,
			isFinished: false,
			barWidth: 0
		}
	},
	computed: {
		computetStatus() {
			return `Вопрос ${this.currentQuestion + 1} из ${this.questions.length}`
		},
		computedQuestion() {
			let index = this.currentQuestion
			return this.questions[index]
		},
		computedFinished() {
			return this.currentQuestion === this.questions.length ? true : false
		},
		computedScore() {
			return this.computedQuestion.right
		},
		computedProgress() {
			return 100 / this.questions.length
		},
		computedBarWidth() {
			return `width: ${this.barWidth + this.computedProgress}%`
		}

	},
	methods: {
		onAnswer(index) {
			if (index === this.computedScore) {
				this.score++
			}
			this.barWidth += this.computedProgress
			this.currentQuestion++
			console.log(this.score)
		},
		onFinish() {
			this.currentQuestion = 0
			this.isFinished = false
			this.barWidth = 0
			this.score = 0
		}
	},
};
</script>

<template>
	<div class="mt-[10vh] max-w-[600px] min-h-[300px] border-gray-100 bg-white mx-auto rounded-md">
		<div v-if="computedFinished" class="p-8 text-center">
			<p class="text-gray-300">Ваш результат: {{ score }}</p>
			<h1 class="text-1xl">Конец</h1>
			<button @click="onFinish" class="py-2 px-4 text-white rounded-md mt-2 hover:bg-blue-500 bg-blue-600">Начать
				сначала</button>
		</div>
		<div v-else class="p-8 text-center">
			<div>
				<p class="text-gray-300">{{ computetStatus }}</p>
				<h1 class="text-1xl">{{ computedQuestion.question }}</h1>
				<div class="text-left mt-8">
					<span>Варианты:</span>
					<div class="h-[1em] border border-gray-100 mt-2">
						<div class="h-[100%] bg-blue-500 transition-all" :style="computedBarWidth"></div>
					</div>
					<ul>
						<li class="text-center w-[100%] border border-gray-100 p-2 mt-2 cursor-pointer"
							v-for="(item, index) in computedQuestion.answers" :key="item" @click="onAnswer(index)">
							{{ item }}
						</li>
					</ul>
				</div>
			</div>
		</div>
	</div>
</template>

<style scoped></style>
