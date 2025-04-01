<script lang="ts">
    interface Option {
        label: string;
        value: string;
        disabled?: boolean;
    }

    interface Props {
        options?: Option[]; // Mark as optional to allow default
        orientation?: "vertical" | "horizontal";
        labelPosition?: "left" | "right";
        value: string;
    }

    let {
        options = [
            { label: "Option 1", value: "option1" },
            { label: "Option 2", value: "option2", disabled: true },
        ],
        orientation = "vertical",
        labelPosition = "right",
        value,
    }: Props = $props();

    let groupId = `radio-${Math.random().toString(36).slice(2)}`;
</script>

<div
    class="radio-group"
    class:horizontal={orientation === "horizontal"}
    role="radiogroup"
    aria-orientation={orientation}
>
    {#each options as option, index}
        <div class="radio-option" class:label-left={labelPosition === "left"}>
            <input
                type="radio"
                id={`radio-${groupId}-${index}`}
                name={groupId}
                value={option.value}
                bind:group={value}
                disabled={option.disabled}
                aria-disabled={option.disabled}
                aria-checked={value === option.value}
                aria-labelledby={`radio-${groupId}-${index}-label`}
            />
            <label
                id={`radio-${groupId}-${index}-label`}
                for={`radio-${groupId}-${index}`}
            >
                {option.label}
            </label>
        </div>
    {/each}
</div>

<style>
    .radio-group {
        display: flex;
        flex-direction: column;
        gap: 0.5rem;
        width: max-content;
        font: "Montserrat", sans-serif;
    }
    .horizontal {
        flex-direction: row;
    }

    .radio-option {
        display: flex;
        align-items: center;
        gap: 0.5rem;
        position: relative;
        transition: all 0.2s ease;
        max-width: content;
    }

    .label-left {
        flex-direction: row-reverse;
    }

    input[type="radio"] {
        appearance: none;
        width: 20px;
        height: 20px;
        border: 1px solid #8e8b9e;
        border-radius: 50%;
        position: relative;
        cursor: pointer;
        transition: all 0.15s ease;
        background-color: transparent;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    /* Checked state */
    input[type="radio"]:checked::before {
        content: "";
        width: 10px;
        height: 10px;
        border-radius: 10px;
        background: var(
            --gradient,
            linear-gradient(
                90deg,
                var(--clr-gradient-start, #4f61df) 0%,
                var(--clr-gradient-end, #9252ff) 100%
            )
        );
        border-radius: 50%;
        transition: background-color 0.2s ease;
    }

    /* Focus visible (keyboard) */
    input[type="radio"]:focus-visible {
        outline: 2px solid #2f2abf;
        outline-offset: 4px;
    }

    /* Hover */
    input[type="radio"]:hover {
        border-color: #3b1fa3;
    }

    /* Active / Pressed */
    input[type="radio"]:active {
        background-color: #eee;
        border-color: #3b1fa3;
    }

    /* Disabled */
    input[type="radio"]:disabled {
        border-color: #ccc;
        background-color: #f5f5f5;
        cursor: not-allowed;
    }

    input[type="radio"]:disabled:checked::before {
        background: #ccc;
    }

    input[type="radio"]:disabled + label {
        color: #aaa;
        cursor: not-allowed;
    }

    label {
        cursor: pointer;
        user-select: none;
    }

    input[type="radio"]:disabled + label {
        cursor: not-allowed;
    }
</style>
