<script>
    import { onMount } from 'svelte';
    import { outputThemeVariables } from "../logic/color";

    import { Theme } from '../stores/status';
    import { customHue } from "../stores/status";

    let hue;
    let defaultHue = 240;

    $: hue = $customHue ? $customHue : defaultHue;

    onMount(() => {
        if (!$Theme) {
            if (window.matchMedia('(prefers-color-scheme: dark)').matches) {
                Theme.set('dark');
            } else {
                Theme.set('light');
            }
        }
    });
</script>

{#key $Theme}
    {@html outputThemeVariables(hue, ":root")}
{/key}