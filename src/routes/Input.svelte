<script lang="ts">
    export let placeholder = "Text input"
    export let handleChange: any

    let value = ""

    $: value = handleChange(value)
</script>

<input bind:value placeholder={placeholder} type="text" />