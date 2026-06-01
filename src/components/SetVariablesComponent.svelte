<script lang="ts">
import type { SvelteWrapperProps } from "@visuallyjs/browser-ui-svelte"

let { model, vertex, data }:SvelteWrapperProps = $props();

function removeNode() {
  model.removeNode(vertex)
}
</script>

<div class="vjs-callflow-node" data-vjs-target="true">
  <div class="vjs-callflow-delete" onclick={removeNode}></div>
  <div class="vjs-callflow-label">
    <div class="vjs-callflow-node-icon" />
    Set Variables
  </div>

  {#each data.variables as variable (variable.id)}
    <div class="vjs-callflow-variable">
      <span class="vjs-callflow-variable-name">{ variable.name }</span>
      =
      <span class="vjs-callflow-variable-value">{ variable.value }</span>
    </div>
  {/each}

  <div class="vjs-callflow-connect" data-vjs-source="true" />
</div>
