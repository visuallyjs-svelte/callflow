<script lang="ts">
import { PaletteComponent } from '@visuallyjs/browser-ui-svelte'
import { NODE_TYPES } from "./node-types"
import type { BrowserElement } from "@visuallyjs/browser-ui"

function dataGenerator(el: BrowserElement) {
  const type = el.getAttribute("data-vjs-type")
  const nodeType = NODE_TYPES.find(nt => nt.type === type)
  const base: any = Object.assign({ type }, Object.assign({}, nodeType?.payload || {}))
  return base
}
</script>

<PaletteComponent className="vjs-callflow-palette" {dataGenerator}>
    {#each NODE_TYPES as nt (nt.type)}
        <div data-vjs-type={nt.type} title="Drag to add new" class="vjs-callflow-palette-item">
			<div class="vjs-callflow-node-icon"></div>
            { nt.label }
        </div>
    {/each}
</PaletteComponent>
