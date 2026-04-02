<script setup lang="ts">
import Header from '@/components/Header.vue';

</script>

<template>
	<section class="min-h-screen bg-gray-100">
		<Header />
		<div class="max-w-4xl mx-auto px-4 py-10 flex items-center justify-center">
			<div class="bg-white rounded-lg shadow-md p-6 md:p-8">
				<h1 class="text-2xl md:text-3xl font-bold text-gray-800">Bienvenue sur QuizMaster</h1>
				<p class="mt-3 text-gray-600 leading-relaxed">
					Cette section utilise un style Tailwind simple pour debutant: fond clair, carte blanche,
					titre visible et espacement propre.
				</p>

				<button
					type="button"
					class="mt-6 bg-indigo-600 text-white px-5 py-2 rounded-md hover:bg-indigo-700 transition-colors"
				>
					Commencer un quiz
				</button>
			</div>
		</div>
	</section>
</template>
