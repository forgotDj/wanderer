<script module lang="ts">
    export type SelectItem = {
        text: string;
        value: any;
    };
</script>

<script lang="ts">
    interface Props {
        name?: string;
        items?: SelectItem[];
        value?: any;
        label?: string;
        disabled?: boolean;
        onchange?: (value: any) => void
    }

    let {
        name = "",
        items = [],
        value = $bindable(items.at(0)?.value ?? ""),
        label = "",
        disabled = false,
        onchange
    }: Props = $props();

    function onChange(target: any) {
        onchange?.(target?.value);
    }
</script>

<div>
    {#if label.length}
        <label for={name} class="text-sm font-medium pb-1">
            {label}
        </label>
    {/if}
    <select
        {name}
        class="block bg-input-background h-10 px-4 border-r-8 border-transparent outline-1 outline-input-border rounded-md focus:outline-input-border-focus transition-colors"
        class:text-gray-500={disabled}
        {disabled}
        bind:value
        onchange={(e) => onChange(e.target)}
    >
        {#each items as item}
            <option value={item.value}>{item.text}</option>
        {/each}
    </select>
</div>
