<script module>
    import {defineMeta} from '@storybook/addon-svelte-csf';
    import Formwrap from './Formwrap.svelte';

    /**
     * The formwrap component is a wrapper for form elements that adds some spacing and padding to the elements.
     * Usage is advised, but not required.
     */
    const {Story} = defineMeta({
        title: 'Handson/Formwrap',
        component: Formwrap,
        tags: ['autodocs'],
        argTypes: {},
        args: {}
    });
</script>
<script>
    import Input from '../input/Input.svelte';
    import Switch from '../switch/Switch.svelte';
</script>

<Story name="Generic" args={{}}>
    <Formwrap>
        <Input label="Text field"/>
        <Input label="Password" type="password"/>
        <Switch label="Switch"/>
    </Formwrap>
</Story>
