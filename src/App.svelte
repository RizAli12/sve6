<script>
  import Hoverable from "./Hoverable.svelte";
  import Project from "./Project.svelte";
  import Comment from "./Comment.svelte";

  import RedThing from "./RedThing.svelte";
  import GreenThing from "./GreenThing.svelte";
  import BlueThing from "./BlueThing.svelte";

  const options = [
    { color: "red", component: RedThing },
    { color: "green", component: GreenThing },
    { color: "blue", component: BlueThing },
  ];

  let selected = options[0];

  import Box from "./Box.svelte";
  export let name;

  import Folder from "./Folder.svelte";

  let root = [
    {
      name: "Important work stuff",
      files: [{ name: "quarterly-results.xlsx" }],
    },
    {
      name: "Animal GIFs",
      files: [
        {
          name: "Dogs",
          files: [{ name: "treadmill.gif" }, { name: "rope-jumping.gif" }],
        },
        {
          name: "Goats",
          files: [{ name: "parkour.gif" }, { name: "rampage.gif" }],
        },
        { name: "cat-roomba.gif" },
        { name: "duck-shuffle.gif" },
        { name: "monkey-on-a-pig.gif" },
      ],
    },
    { name: "TODO.md" },
  ];
</script>

<main>
  <h1>Hello {name}!</h1>

  <h1>Projects</h1>

  <ul>
    <li>
      <Project
        title="Add Typescript support"
        tasksCompleted={25}
        totalTasks={57}
      >
        <div slot="comments">
          <Comment
            name="Ecma Script"
            postedAt={new Date("2020-08-17T14:12:23")}
          >
            <p>Those interface tests are now passing.</p>
          </Comment>
        </div>
      </Project>
    </li>
    <li>
      <Project
        title="Update documentation"
        tasksCompleted={18}
        totalTasks={21}
      />
      <Box>
        <select bind:value={selected}>
          {#each options as option}
            <option value={option}>{option.color}</option>
          {/each}
        </select>

        <svelte:component this={selected.component} />
      </Box>

      <Box />
    </li>
  </ul>

  <p>
    Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn
    how to build Svelte apps.
  </p>

  <Hoverable let:hovering={active}>
    <div class:active>
      {#if active}
        <p>I am being hovered upon.</p>
      {:else}
        <p>Hover over me!</p>
      {/if}
    </div>
  </Hoverable>

  <Hoverable let:hovering={active}>
    <div class:active>
      {#if active}
        <p>I am being hovered upon.</p>
      {:else}
        <p>Hover over me!</p>
      {/if}
    </div>
  </Hoverable>

  <Hoverable let:hovering={active}>
    <div class:active>
      {#if active}
        <p>I am being hovered upon.</p>
      {:else}
        <p>Hover over me!</p>
      {/if}
    </div>
  </Hoverable>

  <Folder name="Home" files={root} expanded />
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }

  h1 {
    font-weight: 300;
    margin: 0 1rem;
  }

  ul {
    list-style: none;
    padding: 0;
    margin: 0.5rem;
    display: flex;
  }

  @media (max-width: 600px) {
    ul {
      flex-direction: column;
    }
  }

  li {
    padding: 0.5rem;
    flex: 1 1 50%;
    min-width: 200px;
  }
  div {
    padding: 1em;
    margin: 0 0 1em 0;
    background-color: #eee;
  }

  .active {
    background-color: #ff3e00;
    color: white;
  }
</style>
