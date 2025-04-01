<script lang="ts">
    import Icon from "../icon/Icon.svelte"; // Pfad zur Icon-Komponente anpassen
    import InputHelper from "../util/InputHelper.svelte"; // Erstellen Sie diese Komponente (siehe unten)
    import FloatingLabel from "../util/FloatingLabel.svelte"; // Erstellen Sie diese Komponente (siehe unten)

    interface Props {
        label: string;
        placeholder?: string;
        description?: string;
        error?: string;
        iconLeft?: string;
        iconRight?: string;
        value: string;
        icon: string;
        disabled?: boolean;
        required?: boolean;
    }

    let {
        label,
        placeholder,
        description,
        error,
        icon = "chevronLeft",
        iconLeft,
        iconRight,
        value,
        disabled,
        required,
        ...restProps
    }: Props = $props();

    let id = `input-${Math.random().toString(36).slice(2)}`;
    let hasFocus = $state(false);
    let isFloating = $derived(hasFocus || !!value || !!placeholder); // Floating auch bei Placeholder
</script>

<div
    class="input-wrapper"
    class:is-disabled={disabled}
    class:has-error={!!error}
>
    <div class="input-box" class:focused={hasFocus}>
        {#if iconLeft}
            <span class="icon left">
                <Icon {icon} />
            </span>
        {/if}

        <FloatingLabel {id} {label} {isFloating} {required} {error} />

        <input
            {id}
            bind:value
            {placeholder}
            {required}
            {disabled}
            aria-invalid={!!error}
            aria-describedby={description || error ? `${id}-helper` : undefined}
            onfocus={() => (hasFocus = true)}
            onblur={() => (hasFocus = false)}
            {...restProps}
        />

        {#if iconRight}
            <span class="icon right">
                <Icon {icon} />
            </span>
        {/if}
    </div>

    <InputHelper {id} {description} {error} />
</div>

<style>
    :global(:root) {
        --border: #d0d5dd;
        --hover: #98a2b3;
        --focus: #6941c6;
        --error: #d92d20;
        --disabled-bg: #f2f4f7;
        --disabled-border: #e4e7ec;
        --text: #101828;
        --label: #667085;
        --placeholder: #98a2b3;
        --helper-text: #667085;
    }

    .input-wrapper {
        display: flex;
        flex-direction: column;
        gap: 0.25rem;
        width: 300px;
    }

    .input-box {
        position: relative;
        display: flex;
        align-items: center;
        border: 1px solid var(--border);
        border-radius: 8px;
        padding: 1rem 1.5rem;
        background: white;
        transition: border-color 0.2s ease;
    }

    .input-box:hover {
        border-color: var(--hover);
    }

    .input-box:active {
        background-color: #f9fafb;
    }

    .focused {
        border-color: var(--focus);
        box-shadow: 0 0 0 2px rgba(105, 65, 198, 0.2);
    }

    .has-error .input-box {
        border-color: var(--error);
    }

    .is-disabled .input-box {
        background-color: var(--disabled-bg);
        border-color: var(--disabled-border);
        pointer-events: none;
    }

    .icon {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        color: var(--label);
    }

    .icon.left {
        left: 1rem;
    }

    .icon.right {
        right: 1rem;
    }

    input {
        appearance: none;
        border: none;
        background: transparent;
        width: 100%;
        font: inherit;
        padding: 0;
        color: var(--text);
        cursor: text;
        padding-left: 0.25rem;
    }

    input:disabled {
        color: var(--placeholder);
        cursor: not-allowed;
    }
</style>
