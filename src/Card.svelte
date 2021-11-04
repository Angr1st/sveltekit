<script>
    export let mission_name;
    export let site_name_long;
    export let rocket_name;
    export let details;
    export let launch_date_local;
</script>

<li>
    <div
      class="card-link"
      target="_blank"
      rel="noopener"
    >
      <h2>{mission_name}</h2>
      <p>{site_name_long}</p>
      <p>{rocket_name}</p>
      {#if details != null}
        <p>{details}</p>
      {/if}
      <p>{new Date(launch_date_local).toLocaleString()}</p>
  </div>
</li>

<style>
      h2 {
    font-size: 18px;
  }

      li {
    border: 1px solid #eaeaea;
    border-radius: 8px;
    margin-bottom: 16px;
    background-color: white;
    transition: 0.15s box-shadow ease-in-out;
  }

  li:hover {
    box-shadow: 0 5px 10px rgba(0, 0, 0, 0.12);
  }

  p {
    color: #666;
    font-size: 14px;
    line-height: 1.75;
  }

  .card-link {
    padding: 8px 24px;
    display: block;
  }
</style>