<script lang="ts">
    interface Option {
        label: string;
        value: string;
    }

    interface Props {
        label: string;
        options?: Option[];
        value: string;
        icon?: string | null;
        error?: string;
        description?: string;
        required?: boolean;
        disabled?: boolean;
    }

    let {
        label,
        options = [],
        value,
        icon = null,
        error = "",
        description = "",
        required = false,
        disabled = false,
        ...restProps
    }: Props = $props();

    let id = `select-${Math.random().toString(36).slice(2)}`;
    let hasFocus = $state(false);
    let isFloating = $derived(hasFocus || !!value);
</script>

<div
    class="select-wrapper"
    class:is-disabled={disabled}
    class:has-error={!!error}
>
    <div class="select-box" class:focused={hasFocus}>
        {#if icon}
            <span class="icon" aria-hidden="true">
                {@html icon}
            </span>
        {/if}

        <select
            {id}
            bind:value
            {required}
            {disabled}
            aria-invalid={!!error}
            aria-describedby={description || error ? `${id}-helper` : undefined}
            onfocus={() => (hasFocus = true)}
            onblur={() => (hasFocus = false)}
            {...restProps}
        >
            <option value="" disabled selected hidden></option>
            {#each options as opt}
                <option value={opt.value}>{opt.label}</option>
            {/each}
        </select>

        <label for={id} class:float={isFloating}>
            {label}{required ? " *" : ""}
        </label>

        <span class="chevron" aria-hidden="true">
            <svg viewBox="0 0 24 24" width="20" height="20">
                <path d="M7 10l5 5 5-5z" fill="currentColor" />
            </svg>
        </span>
    </div>
    {#if description || error}
        <div id={`${id}-helper`} class="helper-text">
            {error || description}
        </div>
    {/if}
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

    .select-wrapper {
        display: flex;
        flex-direction: column;
        gap: 0.25rem;
        width: 300px; /* Adjust width as needed */
    }

    .select-box {
        position: relative;
        display: flex;
        align-items: center;
        border: 1px solid var(--border);
        border-radius: 8px;
        padding: 1rem 1.5rem; /* Reduced padding */
        background: white;
        transition: border-color 0.2s ease;
    }

    .select-box:hover {
        border-color: var(--hover);
    }

    .select-box:active {
        background-color: #f9fafb;
    }

    .focused {
        border-color: var(--focus);
        box-shadow: 0 0 0 2px rgba(105, 65, 198, 0.2);
    }

    .has-error .select-box {
        border-color: var(--error);
    }

    .is-disabled .select-box {
        background-color: var(--disabled-bg);
        border-color: var(--disabled-border);
        pointer-events: none;
    }

    .icon {
        position: absolute;
        left: 1rem;
        top: 50%;
        transform: translateY(-50%);
        color: var(--label);
    }

    select {
        appearance: none;
        border: none;
        background: transparent;
        width: 100%;
        font: inherit;
        padding: 0;
        color: var(--text);
        cursor: pointer;
        padding-left: 0.25rem; /* Add some left padding */
    }

    select:disabled {
        color: var(--placeholder);
        cursor: not-allowed;
    }

    label {
        position: absolute;
        left: 1.5rem; /* Adjusted left padding */
        top: 0.6rem; /* Adjusted top padding */
        font-size: 0.875rem; /* Adjusted font size */
        color: var(--label);
        pointer-events: none;
        transition: all 0.2s ease;
        background-color: white; /* Added background to cover border */
        padding: 0 0.25rem; /* Added padding to cover border */
    }

    label.float {
        top: -0.5rem; /* Adjusted top padding */
        font-size: 0.75rem;
        color: var(--focus);
    }

    .has-error label.float {
        color: var(--error);
    }

    .chevron {
        position: absolute;
        right: 1rem;
        top: 50%;
        transform: translateY(-50%) rotate(0deg);
        transition: transform 0.2s ease;
        color: var(--label);
        pointer-events: none;
    }

    .focused .chevron {
        transform: translateY(-50%) rotate(180deg);
        color: var(--focus);
    }

    .has-error .chevron {
        color: var(--error);
    }

    .is-disabled label,
    .is-disabled .chevron {
        color: var(--placeholder);
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
