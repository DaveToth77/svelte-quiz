
<script>
	import Modal from './modal.svelte';
    import { score} from './store.js';
    import { fade, blur, fly, slide, scale } from "svelte/transition";
    import { onMount, beforeUpdate, afterUpdate, onDestroy } from "svelte";
    import Question from "./question.svelte";

    let activeQuestion = 0
    let quiz = getQuiz()
    let isModalOpen = false;



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



const resetQuiz = () => {
    isModalOpen = false
    score.set(0)    
    activeQuestion = 0
    quiz = getQuiz()
}

$: if ($score > 0) {
    isModalOpen = true
}

$: questionNumber = activeQuestion + 1

    </script>

<style>
    .fadeWrapper {
        position: absolute;
    }

</style>

<div>
    <button on:click ={resetQuiz}>Start New Quiz</button>
  
    <h3>My Score: {$score}</h3>
    <h4>Question #{questionNumber}</h4>
  
    {#await quiz}
      Loading....
    {:then data}
  
      {#each data.results as question, index}
        {#if index === activeQuestion}
          <div in:fly={{ x: 100 }} out:fly={{ x: -200 }} class="fadeWrapper">
            <Question  {nextQuestion} {question} />
          </div>
        {/if}
      {/each}
  
    {/await}
</div>
  
{#if isModalOpen}

    <Modal on:close={resetQuiz}>
        <h2>You Won!</h2>
        <p>Congratulations</p>
        <button on:click={resetQuiz}>Start Over</button>
    </Modal>

{/if}


