<script>
export let question = {}
export let nextQuestion;
export let addToScore;

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
    if (!isAnswered) {
        isCorrect = correct
        isAnswered = true
    
    if(correct){
        addToScore()
        }
    }
}



</script>


<h3>
    {@html question.question}
</h3>
{#if isAnswered}
<h5>
    {#if isCorrect }
    You got it right!
    {:else}
        Wrong...Wrong, Wrong, Wrong!
    {/if}
</h5>
{/if}


{#each allAnswers as answer}
<ol>
     <button on:click={() => checkQuestion(answer.correct)}>{@html answer.answer}</button>
</ol>
{/each}

{#if isAnswered}
    <div>
        <button on:click={nextQuestion}>Next Question</button>
    </div>
{/if}
