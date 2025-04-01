<script module>
    import { defineMeta } from "@storybook/addon-svelte-csf";
    import Input from "./Input.svelte";

    const { Story } = defineMeta({
        title: "Handson/Input",
        component: Input,
        tags: ["autodocs"],
        argTypes: {},
    });
</script>

<Story name="Generic" args={{}}></Story>
