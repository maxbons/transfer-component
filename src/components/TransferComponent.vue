<template>
    <div class="container">
        <div>
            <div class="header">
                <strong>Source</strong>
                <span>{{ source.length }} items</span>
            </div>
            <div class="select-box">
                <input
                    v-model="querySource"
                    class="searchbar"
                    type="text"
                    placeholder="search here"
                    @input="handleSearch('left', querySource)"
                />
                <div v-for="item in source">
                    <input
                        id="checkbox"
                        type="checkbox"
                        v-model="item.checked"
                    />
                    <label for="checkbox">
                        {{ item.name }}
                    </label>
                </div>
            </div>
        </div>

        <div class="buttons-wrapper">
            <button type="button" @click="transfer('right')">--></button>
            <button type="button" @click="transfer('left')"><--</button>
        </div>

        <div>
            <div class="header">
                <strong>Target</strong>
                <span>{{ target.length }} items</span>
            </div>
            <div class="select-box">
                <input
                    v-model="queryTarget"
                    class="searchbar"
                    type="text"
                    placeholder="search here"
                    @input="handleSearch('right', queryTarget)"
                />
                <div v-for="item in target">
                    <input
                        id="checkbox"
                        type="checkbox"
                        v-model="item.checked"
                    />
                    <label for="checkbox">
                        {{ item.name }}
                    </label>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Fuse from 'fuse.js';

export default {
    name: 'TransferComponent',

    props: {
        dataLeft: {
            type: Array,
            default: [],
        },
        dataRight: {
            type: Array,
            default: [],
        },
    },

    data() {
        return {
            source: [],
            target: [],
            querySource: '',
            queryTarget: '',
        };
    },

    watch: {
        querySource() {
            if (!this.querySource) {
                this.source = this.dataLeft;
            }
        },
        queryTarget() {
            if (!this.queryTarget) {
                this.target = this.dataRight;
            }
        },
    },

    created() {
        this.source = this.dataLeft;
        this.target = this.dataRight;
    },

    methods: {
        transfer(direction) {
            switch (direction) {
                case 'right':
                    this.moveItems(this.source, this.target);
                    this.source = this.source.filter(
                        (item) => item.checked === false
                    );
                    this.updateLists();
                    break;
                case 'left':
                    this.moveItems(this.target, this.source);
                    this.target = this.target.filter(
                        (item) => item.checked === false
                    );
                    this.updateLists();
                    break;
            }
        },

        moveItems(source, target) {
            source.forEach((item) => {
                if (item.checked) {
                    target.push({
                        name: item.name,
                        checked: false,
                    });
                }
            });
        },

        updateLists() {
            const data = {
                left: this.source,
                right: this.target,
            };
            this.$emit('update-lists', data);
        },

        handleSearch(direction, query) {
            const list = direction === 'left' ? this.source : this.target;
            const fuse = new Fuse(list, {
                keys: ['name'],
            });
            const result = fuse.search(query);

            if (result.length) {
                const newList = [];
                result.forEach((item) => {
                    newList.push(item.item);
                });
                direction === 'left'
                    ? (this.source = newList)
                    : (this.target = newList);
            }
        },
    },
};
</script>

<style>
.container {
    display: flex;
    width: 90%;
    border: 1px solid lightgrey;
    padding: 2rem;
}

.header {
    display: flex;
    justify-content: space-between;
    padding: 0.5rem;
    border: 1px solid lightgrey;
    border-bottom: 0;
}

.select-box {
    height: 200px;
    width: 200px;
    padding: 0.5rem;
    overflow-y: scroll;
    border: 1px solid lightgrey;
}

.searchbar {
    height: 1.5rem;
    max-width: 95%;
    margin-bottom: 0.5rem;
}

.buttons-wrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;
    margin-left: 1rem;
    margin-right: 1rem;
}
</style>
