<script>
    import Question from "./question.svelte";
    let activeQuestion = 0
    let score = 0
    let quiz = getQuiz()


async function getQuiz() {
    const res = await fetch(
        'https://opentdb.com/api.php?amount=10&category=9&difficulty=medium&type=multiple'
        )
     const quiz = await res.json()
    return quiz
}


const nextQuestion = () => {
    activeQuestion++
}

const addToScore = () => {
    score++
    }


const resetQuiz = () => {
    score = 0
    activeQuestion = 0
    quiz = getQuiz()
}
    </script>

<style>

</style>

<div>
    <button on:click={resetQuiz}>Start New Quiz</button>
    
<h1>My Score: {score}</h1>
<h1>Question #{activeQuestion + 1}</h1>
    {#await quiz}
        Loading...
    {:then data}

    {#each data.results as question, index}
    {#if index === activeQuestion}
        <Question {addToScore} {nextQuestion} {question}/>
    {/if}
    {/each}
    {/await}






</div>
