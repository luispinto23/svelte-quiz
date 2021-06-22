<script>
  import Question from './Question.svelte';

  let quiz = getQuiz();

  async function getQuiz() {
    const res = await fetch('https://opentdb.com/api.php?amount=10&category=12&type=multiple');
    const quiz = await res.json();

    return quiz;
  }

  function handleClick() {
    quiz = getQuiz();
  }
</script>

<div>
  <button on:click={handleClick}>Start Quiz</button>

  {#await quiz}
    <h3>Loading...</h3>
  {:then data}
    {#each data.results as apiQuestion}
       <Question {apiQuestion}/>
    {/each}
  {/await}

  
</div>

<style>
  h4 {
    color: red;
  }
</style>