<script lang="ts">
    let input: HTMLInputElement;
    let wrapper: HTMLDivElement;

    export let shift: () => void;
    export let type: "number" | "empty" | "button" = "number";
    export let index:number;

    const n1 = Math.floor(Math.random() * 10);
    const n2 = Math.floor(Math.random() * 10);

let correct = false;
let wrong = false;

    function validate() {
        const arr1 = input.value.split("");
        const arr2 = String(n1 * n2).split("");
        if (!arr1.every((val, i) => val === arr2[i])) {
            // wrong
            wrong = true
            shift();
        }
        if (input.value === String(n1 * n2)) {
            // correct
            correct = true
            shift();
        }
    }
    $: index, (()=>{if(input && index === 2){input.disabled=false; input.focus()}; console.log(input)})();
</script>

<div
    bind:this={wrapper}
    class="
    {correct ? "bg-green-500":wrong?"bg-red-500":""}
    rounded-xl transition-all absolute
    w-full py-4
    font-semibold text-9xl text-center whitespace-nowrap
    "
    style="
        transform: translate(0,{(index-2)*15}rem) scale({1/ Math.pow(2,Math.abs(index-2))});
        opacity: {1/ (Math.abs(index-2)+1)};
    "
>
    {#if type === "number"}
        {n1} * {n2} =
        <input
            bind:this={input}
            on:input={validate}
            disabled={index !== 2}
            type="text"
            class="bg-transparent w-40"
        />
    {:else if type === "button"}
        <button on:click={shift}> play </button>
    {/if}
</div>
