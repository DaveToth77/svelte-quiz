<script>
    import Question from "./question.svelte";
let quiz = getQuiz()


async function getQuiz() {
    const res = await fetch(
        'https://opentdb.com/api.php?amount=10&category=9&difficulty=medium&type=multiple'
        )
     const quiz = await res.json()
    return quiz
}

const handleClick = () => {
    quiz = getQuiz()
}
    </script>

<style>

</style>

<div>
    <button on:click={handleClick}>Get New Questions</button>
    

    {#await quiz}
        Loading...
    {:then data}

    {#each data.results as question}

    <Question {question}/>
    {/each}

{/await}





</div>
