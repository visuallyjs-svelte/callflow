<script lang="ts">
import { type CallFlowVariable } from "./definitions"
import { uuid, type Vertex } from "@visuallyjs/browser-ui"

let { obj, onSave, onCancel } = $props<{
    obj: Vertex,
    onSave: (variables: Array<CallFlowVariable>) => void,
    onCancel: () => void
}>();

let variables = $state<Array<CallFlowVariable>>(obj.data.variables.map((v: CallFlowVariable) => Object.assign({}, v)));

let newVariableNameInput: HTMLInputElement;
let newVariableValueInput: HTMLInputElement;

$effect(() => {
    variables = obj.data.variables.map((v: CallFlowVariable) => Object.assign({}, v));
});

function addVariable() {
  if (newVariableNameInput && newVariableValueInput && newVariableNameInput.value.length > 0 && newVariableValueInput.value.length > 0) {
    variables.push({
      name: newVariableNameInput.value,
      value: newVariableValueInput.value,
      id: uuid()
    })
    newVariableNameInput.value = ""
    newVariableValueInput.value = ""
  }
}

function deleteVariable(id: string) {
  variables = variables.filter((v: CallFlowVariable) => v.id !== id)
}

function setName(id: string, event: Event) {
  const target = event.target as HTMLInputElement
  const variable = variables.find(v => v.id === id)
  if (variable) {
    variable.name = target.value
  }
}

function setValue(id: string, event: Event) {
  const target = event.target as HTMLInputElement
  const variable = variables.find(v => v.id === id)
  if (variable) {
    variable.value = target.value
  }
}

function commit() {
  onSave(variables)
}

</script>

<table>
    <thead>
      <tr>
        <th>Name</th>
        <th>Value</th>
        <th />
      </tr>
    </thead>
    <tbody>
      {#each variables as variable (variable.id)}
          <tr>
            <td><input value={variable.name} type="text" onblur={(e) => setName(variable.id, e)} /></td>
            <td><input value={variable.value} type="text" onblur={(e) => setValue(variable.id, e)} /></td>
            <td><button onclick={() => deleteVariable(variable.id)}>✖</button></td>
          </tr>
      {/each}

      <tr>
        <td colspan="2">
          <hr style="color:whitesmoke" />
        </td>
      </tr>

      <tr>
        <td><input placeholder="new variable name" type="text" bind:this={newVariableNameInput} /></td>
        <td><input placeholder="new variable value" type="text" bind:this={newVariableValueInput} /></td>
        <td><button onclick={addVariable}>+</button></td>
      </tr>
    </tbody>
  </table>
  <div class="vjs-callflow-set-variables-buttons">
    <button onclick={commit}>Save</button>
    <button onclick={onCancel}>Cancel</button>
  </div>
