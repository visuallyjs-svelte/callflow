<script lang="ts">
import {
    SurfaceProvider,
    SurfaceComponent,
    ControlsComponent,
    MiniviewComponent
} from "@visuallyjs/browser-ui-svelte"

import renderOptions from './render-options'
import viewOptions from './view-options'
import modelOptions from './model-options'

import CallFlowPalette from "./CallFlowPalette.svelte";
import CallflowInspector from "./Inspector.svelte";

let url = "/callflow.json"

</script>

<div class="vjs-callflow">
    <SurfaceProvider>
        <SurfaceComponent className="vjs-callflow-canvas"
                              renderOptions={renderOptions}
                              viewOptions={viewOptions}
                              modelOptions={modelOptions}
                              {url}>

            <ControlsComponent/>
            <MiniviewComponent/>
        </SurfaceComponent>
        <div class="vjs-callflow-rhs">
            <CallFlowPalette/>
            <CallflowInspector/>
        </div>

    </SurfaceProvider>
</div>
