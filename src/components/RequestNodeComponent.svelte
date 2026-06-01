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
    Request
  </div>
  <div class="vjs-callflow-request-url">
    { data.url }
  </div>
  <div class="vjs-callflow-request-port" data-vjs-port="condition">
    <span>condition</span>
    <div class="vjs-callflow-connect" data-vjs-source="true" />
  </div>
  <div class="vjs-callflow-request-port" data-vjs-port="else">
    <span>Else</span>
    <div class="vjs-callflow-connect vjs-callflow-fail-path" data-vjs-source="true" />
  </div>
  <div class="vjs-callflow-request-port" data-vjs-port="failure">
    <span>Failure</span>
    <div class="vjs-callflow-connect vjs-callflow-fail-path" data-vjs-source="true" />
  </div>
</div>
