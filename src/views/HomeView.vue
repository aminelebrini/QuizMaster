<script lang="ts">
import Header from '@/components/Header.vue'

export default {
	name: 'HomeView',
	components: {
		Header,
	},
	data() {
		return {
			openquiz: false,
			closeintro: true,
			quizData: null as null | { difficulty: string; question: string, incorrect_answers: string[], correct_answer: string },
            answer: '',
            points: 0,
			choices: [] as string[],
            isTrue: false,
			lastCorrectAnswer: '',
		}
	},
	methods: {
		toggle(modalName: string) {
			if (modalName === 'openquiz') {
				this.openquiz = !this.openquiz
                this.closeintro = !this.closeintro
			}
		},
		async fetchdata() {
			try {
				const response = await fetch('https://opentdb.com/api.php?amount=1&type=multiple')
				const data = await response.json()
				this.quizData = data?.results?.[0] ?? null
				if (this.quizData) {
					this.choices = [...this.quizData.incorrect_answers, this.quizData.correct_answer]
					for (let j = this.choices.length - 1; j > 0; j -= 1) {
						const k = Math.floor(Math.random() * (j + 1))
						const temp = this.choices[j]!
						this.choices[j] = this.choices[k]!
						this.choices[k] = temp
					}
					this.answer = ''
				}
			} catch (error) {
				console.error('Error fetching quiz data:', error)
				this.quizData = null
				this.choices = []
			}
		},
        handleAnswerSubmit():void
        {
			if (!this.answer || !this.quizData) {
				return
			}
			const currentCorrectAnswer = this.quizData.correct_answer
            if(this.answer === this.quizData?.correct_answer)
            {
                this.points += 1;
                this.isTrue = false;
				this.lastCorrectAnswer = ''
            }
            else
            {
                this.points -= 1;
                this.isTrue = true;
				this.lastCorrectAnswer = currentCorrectAnswer
            }
            this.fetchdata();
		},

	},
	mounted() {
		this.fetchdata()
	},
}
</script>

<template>
	<section class="min-h-screen bg-gray-100">
		<Header />
		<div v-if="closeintro" class="max-w-4xl mx-auto px-4 py-10 flex items-center justify-center">
			<div class="bg-white rounded-lg shadow-md p-6 md:p-8">
				<h1 class="text-2xl md:text-3xl font-bold text-gray-800">Bienvenue sur QuizMaster</h1>
				<p class="mt-3 text-gray-600 leading-relaxed">
					Cette section utilise un style Tailwind simple pour debutant: fond clair, carte blanche,
					titre visible et espacement propre.
				</p>

				<button
					type="button" @click="toggle('openquiz')"
					class="mt-6 bg-indigo-600 text-white px-5 py-2 rounded-md hover:bg-indigo-700 transition-colors">
					Commencer un quiz
				</button>
			</div>
		</div>
		<div v-if="openquiz" class="max-w-4xl mx-auto px-4 py-10 flex items-center justify-center">
			<div class="w-full max-w-2xl bg-white rounded-lg shadow-md p-6 md:p-8 text-center">
				<div class="flex items-center justify-between mb-4">
					<h2 class="text-2xl md:text-3xl font-bold text-gray-800">Quiz ouvert !</h2>
					<p class="text-sm font-semibold text-indigo-700 bg-indigo-100 px-3 py-1 rounded-full border border-indigo-200">
						Points: {{ points }}
					</p>
				</div>
				<div v-if="quizData && quizData.difficulty === 'easy'" class="mt-4 rounded bg-green-50 p-3 text-green-700">
					Question facile detectee
				</div>
				<div v-if="quizData" class="mt-4 text-left text-gray-700" v-html="quizData.question"></div>
				<form @submit.prevent="handleAnswerSubmit()" class="mt-4 text-left">
					<label
						v-for="choice in choices"
						:key="choice"
						class="mt-2 flex items-center gap-3 w-full px-4 py-2 border rounded-md cursor-pointer hover:bg-gray-50"
					>
						<input
							type="radio"
							name="quiz-answer"
							v-model="answer"
							:value="choice"
						/>
						<span v-html="choice"></span>
					</label>

					<p v-if="choices.length === 0" class="mt-2 text-sm text-gray-500">Chargement des choix...</p>
					<p v-if="isTrue" class="mt-2 text-[15px] text-red-500 font-bold">Bonne réponse : {{ lastCorrectAnswer }} !</p>
                    <button type="submit" class="mt-4 bg-indigo-600 text-white px-5 py-2 rounded-md hover:bg-indigo-700 transition-colors">
                        Soumettre
                    </button>
                </form>
				<button
					type="button"
					@click="toggle('openquiz')"
					class="mt-6 bg-gray-200 text-gray-800 px-5 py-2 rounded-md hover:bg-gray-300 transition-colors">
					Retour
				</button>
			</div>
		</div>
	</section>
</template>