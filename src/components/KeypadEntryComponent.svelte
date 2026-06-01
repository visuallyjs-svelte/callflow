<script lang="ts">
import { ALL_KEYS } from "../constants"
import type { SvelteWrapperProps } from "@visuallyjs/browser-ui-svelte"

let { model, vertex }:SvelteWrapperProps = $props();

function removeNode() {
  model.removeNode(vertex)
}
</script>

<div class="vjs-callflow-node" data-vjs-target="true">
  <div class="vjs-callflow-delete" onclick={removeNode}></div>
  <div class="vjs-callflow-label">
    <div class="vjs-callflow-node-icon" />
    Keypad Entry
  </div>
  <div class="vjs-callflow-keypad">
    {#each ALL_KEYS as k (k)}
      <div class="vjs-callflow-keypad-key" data-vjs-port={k}>
        <span>{ k }</span>
        <div class="vjs-callflow-connect" data-vjs-source="true" />
      </div>
    {/each}
  </div>
</div>
