<template>
    <div id="app">
        <h1>Code assignment:</h1>
        <h2>Transfer component</h2>

        <TransferComponent
            :data-left="collegues"
            :data-right="friends"
            @updateLists="updateLists"
        />
    </div>
</template>

<script>
import TransferComponent from './components/TransferComponent.vue';

export default {
    name: 'App',

    components: {
        TransferComponent,
    },

    data() {
        return {
            collegues: [
                {
                    name: 'Luuk',
                    checked: false,
                },
                {
                    name: 'Shaldi',
                    checked: false,
                },
                {
                    name: 'Arie',
                    checked: false,
                },
                {
                    name: 'Tobias',
                    checked: false,
                },
                {
                    name: 'Sjors',
                    checked: false,
                },
            ],
            friends: [
                {
                    name: 'Mark',
                    checked: false,
                },
                {
                    name: 'Jan',
                    checked: false,
                },
                {
                    name: 'Toms',
                    checked: false,
                },
                {
                    name: 'Rolands',
                    checked: false,
                },
            ],
        };
    },

    methods: {
        updateLists(data) {
            this.collegues = data.left;
            this.friends = data.right;
        },
    },
};
</script>
