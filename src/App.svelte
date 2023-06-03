<script lang="ts">
    import { bind } from "svelte/internal";
import PlayBox from "./lib/playBox.svelte";

    let types: Array<{ index: number; type: "number" | "empty" | "button" }> = [
        { index: 0, type: "number" },
        { index: 1, type: "number" },
        { index: 2, type: "button" },
        { index: 3, type: "empty" },
        { index: 4, type: "empty" },
    ];
    function shift() {
        types = [
            { index: types[types.length - 1].index + 1, type: "number" },
            ...types.slice(0,-1)
        ];
    }
</script>

<main
    class="
    w-screen h-screen
    flex justify-center items-center
    "
>
    <div class="background -z-50">
        <div
            class="absolute inset-0 bg-gradient-to-br from-slate-100 to-slate-400"
        />
        <div
            class="absolute inset-0"
            style="
        background-image: radial-gradient(#0003 5%, transparent 5%);
        background-position: 0 0;
        background-size: 20px 20px;
    "
        />
    </div>
    <div
        class="
    w-1/3 h-full
    bg-slate-50 shadow-2xl overflow-hidden
    flex justify-center items-center relative
    "
    >
        {#each types as type, index (type.index)}
            <PlayBox {shift} type={type.type} {index}/>
        {/each}
    </div>
</main>

<style>
</style>
