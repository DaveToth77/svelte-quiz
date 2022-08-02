<script>
let result = ""
let correctAnswer = 'b'
let answers = ["a", "b", "c", "d"]
let quiz = getQuiz()

const pickAnswer = (answer) => {
    if(answer === correctAnswer){
    return result = "Correct!"
    } else {
        result = "Seriously?"
    }
};

async function getQuiz() {
    const res = await fetch(
        'https://opentdb.com/api.php?amount=10&category=9&difficulty=medium&type=multiple'
        )
     const quiz = await res.json()
    // debugger
    return quiz
}

const handleClick = () => {
    quiz = getQuiz()
}
    </script>

<style>
 h4 {
    color: red;
    }
</style>

<div>
    <button on:click={handleClick}>Get New Questions</button>
    {#if result}
        <h4>{result}</h4>
        {:else}
            <h5>Please pick an answer</h5>
    {/if}

{#await quiz}
Loading...
{:then data}

<h3>{data.results[0].question}</h3>
{/await}





    {#each answers as answer}
        <button on:click={() => pickAnswer(answer)}>Answer {answer.toUpperCase()}</button>
    {/each}
</div>
