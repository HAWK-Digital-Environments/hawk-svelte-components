<script lang="ts">
    interface Props {
        id: string;
        label: string;
        isFloating: boolean;
        required?: boolean;
        error?: string;
    }

    let { id, label, isFloating, required, error }: Props = $props();
</script>

<label for={id} class:float={isFloating}>
    {label}{required ? " *" : ""}
</label>

<style>
    :global(:root) {
        --label: #667085;
        --focus: #6941c6;
        --error: #d92d20;
    }

    label {
        position: absolute;
        left: 1.5rem;
        top: 0.6rem;
        font-size: 0.875rem;
        color: var(--label);
        pointer-events: none;
        transition: all 0.2s ease;
        background-color: white;
        padding: 0 0.25rem;
    }

    label.float {
        top: -0.5rem;
        font-size: 0.75rem;
        color: var(--focus);
    }

    .has-error label.float {
        color: var(--error);
    }
</style>
