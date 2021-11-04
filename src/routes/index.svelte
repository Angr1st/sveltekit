<script context="module">
  import Card from '../Card.svelte';

  export async function load({ fetch }) {
    const res = await fetch('https://api.spacex.land/graphql', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        query: `{
          launchesUpcoming(limit: 10, order: "launch_date_utc") {
            details
            launch_site {
              site_name_long
            }
            mission_name
            rocket {
              rocket_name
            }
            launch_date_local
          }
        }`
      })
    });

    if (res.ok) {
      const { data } = await res.json();
      return {
        props: {
          launches: data.launchesUpcoming
        }
      };
    }

    return {
      status: res.status,
      error: new Error(`Error fetching GraphQL data`)
    };
  }
</script>

<script>
  export let launches;
</script>

<h1>Upcoming SpaceX Launches</h1>
<p>
  This is an example <a
    class="link"
    target="_blank"
    rel="noopener"
    href="https://svelte.dev">SvelteKit</a
  >
  application fetching GraphQL data from the public
  <a
    class="link"
    target="_blank"
    rel="noopener"
    href="https://api.spacex.land/graphql">SpaceX API</a
  >. View source on
  <a
    class="link"
    target="_blank"
    rel="noopener"
    href="https://github.com/leerob/sveltekit-graphql">GitHub</a
  >.
</p>
<ul>
  {#each launches as launch}
    <Card mission_name={launch.mission_name} site_name_long={launch.launch_site.site_name_long} rocket_name={launch.rocket.rocket_name} details={launch.details} launch_date_local={launch.launch_date_local}/>
  {/each}
</ul>
<footer>
  <p>
    Created with <a
      class="link"
      target="_blank"
      rel="noopener"
      href="https://svelte.dev">SvelteKit</a
    >
    and deployed with
    <a class="link" target="_blank" rel="noopener" href="https://vercel.com"
      >▲ Vercel</a
    >.
  </p>
</footer>

<style>
  :global(body) {
    font-family: Menlo, Consolas, Monaco, Liberation Mono, Lucida Console,
      monospace;
    background-color: #fafafa;
    max-width: 650px;
    margin: 32px auto;
    padding: 0 16px;
  }
  h1 {
    letter-spacing: -0.025em;
  }
  ul {
    list-style: none;
    padding: 0;
    margin-top: 32px;
  }

  a {
    color: #0070f3;
    text-decoration: none;
  }

  .link {
    transition: 0.15s text-decoration ease-in-out;
    color: #0761d1;
  }
  .link:hover {
    text-decoration: underline;
  }
</style>
