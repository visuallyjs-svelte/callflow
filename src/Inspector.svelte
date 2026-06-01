<script lang="ts">
import {isNode, isPort, type Base, type Vertex, } from "@visuallyjs/browser-ui"
import { PROPERTY_TEXT, PROPERTY_URL, TYPE_CONDITIONS, PROPERTY_NUMBER, TYPE_CALL_FORWARD, TYPE_PLAY_AUDIO, TYPE_REQUEST, TYPE_SET_VARIABLES } from "./constants"
import SetValuesInspectorComponent from "./SetValuesInspectorComponent.svelte"
import {BrowserUISvelteModel, InspectorComponent, useVisuallyJsModel} from "@visuallyjs/browser-ui-svelte";

let currentObj = $state<Vertex>()
let currentType = $state('')

let model = $state<BrowserUISvelteModel>()
useVisuallyJsModel().then((s:BrowserUISvelteModel) => model = s)

function renderEmptyContainer() {
  currentType = ''
}

const portTypeMap: Record<string, string> = {
  [TYPE_CONDITIONS]: "condition"
}

function refresh(obj: Base) {
  if (isNode(obj)) {
    currentType = obj.type
  } else if (isPort(obj)) {
    currentType = portTypeMap[obj.getParent().type]
  }
  currentObj = obj as Vertex
}

function updateVariables(variables: Array<any>) {
    if (currentObj) {
        model!.updateNode(currentObj, { variables })
        model!.clearSelection()
    }
}

function cancel() {
    if (currentObj) {
        model!.clearSelection()
    }
}
</script>

<InspectorComponent className="vjs-callflow-inspector" {refresh} {renderEmptyContainer}>
    {#if currentType === TYPE_PLAY_AUDIO}
      <span>Text:</span>
      <textarea rows="10" cols="10" vjs-att={PROPERTY_TEXT} vjs-focus="true" placeholder="enter text to speak..." ></textarea>
    {/if}

    {#if currentType === TYPE_REQUEST}
      <span>URL:</span>
      <input type="text" vjs-att={PROPERTY_URL} vjs-focus="true" placeholder="enter request URL..." />
    {/if}

    {#if currentType === TYPE_CALL_FORWARD}
      <span>Phone Number:</span>
      <input type="text" vjs-att={PROPERTY_NUMBER} vjs-focus="true" placeholder="enter phone number..." />
    {/if}

    {#if currentType === TYPE_SET_VARIABLES && currentObj}
      <SetValuesInspectorComponent obj={currentObj} onSave={updateVariables} onCancel={cancel} />
    {/if}

    {#if currentType === 'condition'}
      <span>Condition:</span>
      <input vjs-att="value" placeholder="enter condition..." vjs-focus="true" />
    {/if}
</InspectorComponent>
