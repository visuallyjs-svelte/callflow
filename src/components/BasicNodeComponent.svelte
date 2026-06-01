<script lang="ts">
import type { SvelteWrapperProps } from "@visuallyjs/browser-ui-svelte"
import { getNodeLabel } from "../node-types"

let { model, vertex, data }:SvelteWrapperProps = $props();

const label = getNodeLabel(vertex.type)

function removeNode() {
  model.removeNode(vertex)
}
</script>

<div class="vjs-callflow-node" data-vjs-target="true">
  <div class="vjs-callflow-delete" onclick={removeNode}></div>
  <div class="vjs-callflow-label">
    <div class="vjs-callflow-node-icon" />
    { label }
  </div>
  {#if data.text}
    <div class="vjs-callflow-node-text">{ data.text }</div>
  {/if}
  <div class="vjs-callflow-connect" data-vjs-source="true" />
</div>
