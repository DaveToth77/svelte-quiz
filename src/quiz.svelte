
<script>
    import { fade, blur, fly, slide, scale } from "svelte/transition";
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

$: if(score > 1) {
    alert('You Won!')
    resetQuiz()
}

$: questionNumber = activeQuestion + 1

    </script>

<style>
    .fadeWrapper {
        position: absolute;
    }

</style>

<div>
    <button on:click={resetQuiz}>Start New Quiz</button>
  
    <h3>My Score: {score}</h3>
    <h4>Question #{questionNumber}</h4>
  
    {#await quiz}
      Loading....
    {:then data}
  
      {#each data.results as question, index}
        {#if index === activeQuestion}
          <div in:fly={{ x: 100 }} out:fly={{ x: -200 }} class="fadeWrapper">
            <Question {addToScore} {nextQuestion} {question} />
          </div>
        {/if}
      {/each}
  
    {/await}
  </div>
  


