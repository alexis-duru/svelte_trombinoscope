<script>
  import PersonCard from "./lib/PersonCard.svelte";

  const persons = [
    {
      name: "Romain",
      surname: "l'Ourson",
      born: "1985-12-31",
      description: "Someone who loves Svelte !",
    },
    {
      name: "Harry",
      surname: "Potter",
      born: "1980-07-31",
      description: "A wizard who defeated He-who-must-not-be-named",
    },
    {
      name: "Steve",
      surname: "Jobs",
      born: "1955-02-24",
      dead: "2011-10-05",
      description: "Someone who loved apples",
    },
    {
      name: "Diego",
      surname: "Maradona",
      born: "1960-10-30",
      dead: "2020-11-25",
      description: "The hand of God",
    },
    {
      name: "Osamu",
      surname: "Tezuka",
      born: "1928-11-03",
      dead: "1989-02-09",
      description: "Astro boy's dad",
    },
    {
      name: "Billie",
      surname: "Eilish",
      born: "2001-12-18",
      description: "Happier then ever",
    },
    {
      name: "Bernard",
      surname: "Minet",
      born: "1953-12-28",
      description: "Un mec musclé",
    },
  ];

  let filteredPersons = persons;
  let showDead = true;
  let selectedPerson = null;

  function filteredName(e) {
    const filter = e.target.value.toLowerCase();
    filteredPersons = persons.filter((person) =>
      `${person.name} ${person.surname}`.toLowerCase().includes(filter)
    );
  }

  function filteredAge(event) {
    const age = event.target.value;
    filteredPersons = persons.filter((person) => {
      const currentYear = new Date().getFullYear();
      const personAge = person.dead
        ? parseInt(person.dead.split("-")[0], 10) -
          parseInt(person.born.split("-")[0])
        : currentYear - parseInt(person.born.split("-")[0]);

      return personAge <= age;
    });
  }

  function filteredDeadPersons() {
    showDead = !showDead;
    filteredPersons = persons.filter((person) => !person.dead || showDead);
  }
</script>

<div class="person-cards">
  {#each filteredPersons as person}
    <PersonCard {person} on:click={() => (selectedPerson = person)} />
  {/each}
</div>

<div class="button__container">
  <input type="text" on:input={filteredName} placeholder="Filter by name" />
  <label>
    <input type="range" min="0" max="100" value="100" on:input={filteredAge} />
    Filter by age
  </label>
  <label>
    <input
      type="checkbox"
      bind:checked={showDead}
      on:click={filteredDeadPersons}
    />
    View deceased persons
  </label>
</div>

<style>
  .person-cards {
    display: flex;
    flex-wrap: wrap;
    max-width: 800px;
    margin: 0 auto;
  }

  .button__container {
    margin-top: 1rem;
    position: absolute;
    top: 0;
    left: 50%;
    transform: translate(-50%);
  }
</style>
