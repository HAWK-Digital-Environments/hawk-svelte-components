<script lang="ts">
    interface Props {
        id: string;
        description?: string;
        error?: string;
    }

    let { id, description, error }: Props = $props();
</script>

{#if description || error}
    <div id={`${id}-helper`} class="helper-text">
        {error || description}
    </div>
{/if}

<style>
    :global(:root) {
        --helper-text: #667085;
        --error: #d92d20;
    }

    .helper-text {
        font-size: 0.75rem;
        color: var(--helper-text);
        margin-top: 0.25rem;
        padding-left: 1.5rem;
    }

    .has-error .helper-text {
        color: var(--error);
    }
</style>
