<script>
  export let apiQuestion;

  let isCorrect;
  let isAnswered = false;

  let answers = apiQuestion.incorrect_answers.map(answer => {
    return {
      answer,
      correct: false
    }
  });


  let allAnswers = [...answers, {
    answer: apiQuestion.correct_answer,
    correct: true
  }];

  shuffle(allAnswers);

  function shuffle(arr) {
    arr.sort(() => Math.random() - 0.5);
  }

  function checkAnswer(correct) {
    isAnswered = true;
    isCorrect = correct;
  }
</script>

<h3>{@html apiQuestion.question}</h3>

{#if isAnswered}
  <h4>
    {#if isCorrect}
      You got it right
    {:else}
      nope kiddo
    {/if}
  </h4>
{/if}

{#each allAnswers as answer}
  <button on:click={() => checkAnswer(answer.correct)} disabled={isAnswered}>{@html answer.answer}</button>
{/each}