<script>
  import Question from "./Question.svelte";

  let quiz = getQuiz();

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

  {#await quiz}
    <h4>Loading...</h4>
  {:then data}
    <!-- <h3>{data.results[0].question}</h3> -->

    {#each data.results as question}
      <Question {question} />
    {/each}

  {:catch error}
    <h4>Failed to load quiz</h4>
  {/await}

</div>
