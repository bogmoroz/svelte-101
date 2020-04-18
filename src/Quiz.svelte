<script>
  let result = "";
  let correctAnswer = "b";
  let answers = ["a", "b", "c", "d"];
  let quiz = getQuiz();

  function pickAnswer(answer) {
    if (answer === correctAnswer) {
      return (result = "Correct!");
    }

    result = "OOPS";
  }

  async function getQuiz() {
    const res = await fetch(
      "https://opentdb.com/api.php?amount=10&category=18&type=multiple"
    );

    const quiz = await res.json();
    return quiz;
  }

  function handleClick() {
    quiz = getQuiz();
  }
</script>

<style>
  h4 {
    color: red;
  }
</style>

<div>
  <button on:click={handleClick}>Get quiz!</button>
  <h4>Quiz</h4>
  {#if result}
    <h4>{result}</h4>
  {:else}
    <h4>Pick an answer</h4>
  {/if}

  {#await quiz}
    <h4>Loading...</h4>
  {:then data}
    <h3>{data.results[0].question}</h3>
  {:catch error}
    <h4>Failed to load quiz</h4>
  {/await}

  {#each answers as answer}
    <button on:click={() => pickAnswer(answer)}>
      Answer {answer.toUpperCase()}
    </button>
  {/each}

</div>
