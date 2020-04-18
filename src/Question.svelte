<script>
  export let question;
  let answers = question.incorrect_answers;
</script>

<h3>
  {@html question.question}
</h3>

{#each answers as answer}
  <p>
    {@html answer}
  </p>
{/each}
