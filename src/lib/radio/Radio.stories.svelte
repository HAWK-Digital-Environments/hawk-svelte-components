<script module>
    import { defineMeta } from "@storybook/addon-svelte-csf";
    import Radio from "./Radio.svelte";

    const { Story } = defineMeta({
        title: "Handson/Radio",
        component: Radio,
        tags: ["autodocs"],
        argTypes: {},
    });
</script>

<Story name="Generic" args={{}}></Story>
