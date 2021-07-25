<script>
  export let props = [];
  export let slots = [];
  export let events = [];
  export let typedefs = [];

  const types = typedefs.map((typedef) => `export ${typedef.ts}`).join("\n\n");
</script>

{#if types}
  <h2>Types</h2>

  <pre>
    <code>
      {types}
    </code>
  </pre>
{/if}

{#if props.length}
  <h2>Props</h2>

  <table>
    <thead>
      <tr>
        <th>Name</th>
        <th>Type</th>
        <th>Default</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      {#each props as prop}
        <tr>
          <td>{prop.name}</td>
          <td><code>{prop.type}</code></td>
          <td>
            {#if prop.value}
              <code>{prop.value}</code>
            {/if}
          </td>
          <td>{@html prop.description ? prop.description : ""}</td>
        </tr>
      {/each}
    </tbody>
  </table>
{/if}

{#if slots.length}
  <h2>Slots</h2>

  <table>
    <thead>
      <tr>
        <th>Name</th>
        <th>Default</th>
        <th>Props</th>
        <th>Fallback</th>
      </tr>
    </thead>
    <tbody>
      {#each slots as slot}
        <tr>
          <td>{slot.default ? "" : slot.name}</td>
          <td>{slot.default ? "Yes" : "No"}</td>
          <td>
            {#if slot.props}
              <code>{slot.props}</code>
            {/if}
          </td>
          <td>
            {#if slot.fallback}
              {@html slot.fallback}
            {/if}
          </td>
        </tr>
      {/each}
    </tbody>
  </table>
{/if}

{#if events.length}
  <h2>Events</h2>

  <table>
    <thead>
      <tr>
        <th>Name</th>
        <th>Type</th>
        <th>Detail</th>
      </tr>
    </thead>
    <tbody>
      {#each events as event}
        <tr>
          <td>{event.name}</td>
          <td><code>{event.type}</code></td>
          <td>
            {#if event.type === "dispatched"}
              <code>{event.detail}</code>
            {/if}
          </td>
        </tr>
      {/each}
    </tbody>
  </table>
{/if}

<style>
  table {
    color: #374151;
    text-align: left;
  }

  pre {
    padding: 0.5rem;
    border-radius: 0.375rem;
    background-color: #d1d5db;
    max-width: 50rem;
    word-wrap: break-word;
    white-space: pre-wrap;
  }

  code {
    color: #111827;
    font-family: ui-sans-serif, system-ui, -apple-system, system-ui, "Segoe UI";
    font-size: 0.875em;
    font-weight: 500;
  }

  table code {
    padding: 0.3rem 0.5rem;
    border-radius: 0.375rem;
    background-color: #d1d5db;
    white-space: nowrap;
  }

  thead {
    border-bottom-color: #d1d5db;
    border-bottom-width: 1px;
    color: #111827;
    font-weight: 600;
  }

  thead th {
    padding-bottom: 0.75em;
    padding-left: 0.75em;
    padding-right: 0.75em;
  }

  thead th:first-child {
    padding-left: 0;
  }

  thead th:last-child {
    padding-right: 0;
  }

  tbody tr {
    border-bottom-color: #e5e7eb;
    border-bottom-width: 1px;
  }
  tbody td {
    padding: 0.75em;
  }

  tbody td:first-child {
    padding-left: 0;
  }

  tbody td:last-child {
    padding-right: 0;
  }
</style>
