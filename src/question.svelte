<script>
export let question = {}

let isCorrect
let isAnswered = false
let answers = question.incorrect_answers.map(answer => {
  return {
    answer,
    correct: false
  }
})

let allAnswers = [
    ...answers,
    {
        answer: question.correct_answer,
        correct: true
    }
]
const shuffle = (array) => {
    array.sort(() => Math.random() - 0.5)
}

shuffle(allAnswers)
    
const checkQuestion = (correct) => {
isCorrect = correct
isAnswered = true
}



</script>


<h3>
    {@html question.question}
</h3>
{#if isAnswered}
<h4>
    {#if isCorrect }
    You got it right!
    {:else}
        Wrong...Wrong, Wrong, Wrong!
    {/if}
</h4>
{/if}


{#each allAnswers as answer}
<ol>
     <button on:click={() => checkQuestion(answer.correct)}>{@html answer.answer}</button>
</ol>
   

{/each}
