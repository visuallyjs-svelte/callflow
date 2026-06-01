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
    <div class="vjs-callflow-node-icon"></div>
    Forward to Phone
  </div>
  {#if data.number != null}
    <div class="vjs-callflow-node-text">
      { data.number }
    </div>
  {/if}
  <div class="vjs-callflow-condition" data-vjs-port="success">
    Success
    <div class="vjs-callflow-connect" data-vjs-source="true" />
  </div>
  <div class="vjs-callflow-condition" data-vjs-port="no-answer">
    No Answer
    <div class="vjs-callflow-connect vjs-callflow-fail-path" data-vjs-source="true" />
  </div>
  <div class="vjs-callflow-condition" data-vjs-port="busy">
    Busy
    <div class="vjs-callflow-connect vjs-callflow-fail-path" data-vjs-source="true" />
  </div>
  <div class="vjs-callflow-condition" data-vjs-port="decline">
    Decline
    <div class="vjs-callflow-connect vjs-callflow-fail-path" data-vjs-source="true" />
  </div>
  <div class="vjs-callflow-condition" data-vjs-port="error">
    Error
    <div class="vjs-callflow-connect vjs-callflow-fail-path" data-vjs-source="true" />
  </div>
</div>
