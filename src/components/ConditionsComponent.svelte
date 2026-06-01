<script lang="ts">
import type { SvelteWrapperProps } from "@visuallyjs/browser-ui-svelte"
import {Node} from "@visuallyjs/browser-ui"

let { model, vertex, data }:SvelteWrapperProps = $props();

const node = vertex as Node

function removeNode() {
  model.removeNode(vertex)
}

function editCondition(id: string) {
  const port = node.getPort(id)
  if (port != null) {
    model.setSelection(port)
  }
}

function removeCondition(id: string) {
  const port = node.getPort(id)
  if (port) {
    model.removePort(port)
  }
}

function addCondition() {
  const order = data.conditions.length
  const id = `${order}`

  model.addNewPort(node, "condition", {
    id,
    order,
    value: "New Condition"
  })

  setTimeout(() => {
    const port = node.getPort(id)
    if (port) {
      model.setSelection(port)
    }
  })
}
</script>

<div class="vjs-callflow-node" data-vjs-target="true">
  <div class="vjs-callflow-delete" onclick={removeNode}></div>
  <div class="vjs-callflow-label">
    <div class="vjs-callflow-node-icon" />
    Conditions
    <div class="vjs-callflow-add-condition" onclick={addCondition}>+</div>
  </div>
  {#each data.conditions as condition (condition.id)}
    <div class="vjs-callflow-condition" data-vjs-port={condition.id}>
      <span onclick={() => editCondition(condition.id)} title={condition.value}>{ condition.value }</span>
      <div class="vjs-callflow-connect" data-vjs-source="true" />
      {#if condition.value !== 'Else'}
        <div class="vjs-edge-delete" onclick={() => removeCondition(condition.id)} />
      {/if}
    </div>
  {/each}
</div>
