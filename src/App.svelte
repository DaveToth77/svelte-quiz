<script>
import Quiz from "./quiz.svelte";

</script>

<main>
	<h1>Trivia quiz</h1>
	<Quiz quizName="New Quiz"/>

</main>

<style>

	:global(body) {
		background: #524763
	}
	h1 {
		text-align: center;
		color: #fff;
	}

	:global(div) {
		background: #fff;
		border-radius: 15px;
		padding: 40px;
	}
</style>
