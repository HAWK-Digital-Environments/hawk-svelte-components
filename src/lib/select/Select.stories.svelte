<script module>
    import { defineMeta } from "@storybook/addon-svelte-csf";
    import Select from "./Select.svelte";

    const { Story } = defineMeta({
        title: "Handson/Select",
        component: Select,
        tags: ["autodocs"],
        argTypes: {},
    });
</script>

<Story name="Generic" args={{}}></Story>
