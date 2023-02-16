<script>
  import { fade } from "svelte/transition";
  export let person;
  export let selected = false;

  function calculateAge(born, dead) {
    const currentYear = new Date().getFullYear();
    const birthYear = parseInt(born.split("-")[0], 10);
    const deathYear = dead ? parseInt(dead.split("-")[0], 10) : currentYear;
    return deathYear - birthYear;
  }
</script>

<button
  class="card"
  class:person-card={selected}
  on:click={() => (selected = !selected)}
>
  <p>{person.name} {person.surname}</p>
  <p>{calculateAge(person.born, person.dead)} years</p>
  {#if selected}
    <div class="details" transition:fade>
      <h1>{person.name} {person.surname}</h1>
      <h2>Born on {person.born}</h2>
      {#if person.dead}
        <h3>Died on {person.dead}</h3>
      {/if}
      <h4>{person.description}</h4>
    </div>
  {/if}
</button>

<style>
  .details {
    height: 100vh;
    widows: 100vw;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    flex-direction: column;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 10;
    background-color: #1a1a1a;
    transition: 0.3s ease-in-out;
  }
</style>
