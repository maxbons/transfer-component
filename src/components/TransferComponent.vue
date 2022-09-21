<template>
    <div class="wrapper">
        <div class="select-box">
            <div v-for="item in itemsLeft">
                <input id="checkbox" type="checkbox" v-model="item.checked" />
                <label for="checkbox">
                    {{ item.name }}
                </label>
            </div>
        </div>

        <div class="buttons-wrapper">
            <button type="button" @click="transfer('right')">-></button>
            <button type="button" @click="transfer('left')"><-</button>
        </div>

        <div class="select-box">
            <div v-for="item in itemsRight">
                <input id="checkbox" type="checkbox" v-model="item.checked" />
                <label for="checkbox">
                    {{ item.name }}
                </label>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'TransferComponent',

    data() {
        return {
            checkedItems: [],
            itemsLeft: [
                {
                    name: 'Max',
                    checked: false,
                },
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
            itemsRight: [],
        };
    },

    methods: {
        transfer(direction) {
            switch (direction) {
                case 'right':
                    this.itemsLeft.forEach((item) => {
                        if (item.checked) {
                            this.itemsRight.push({
                                name: item.name,
                                checked: false,
                            });
                        }
                    });
                    this.itemsLeft = this.itemsLeft.filter(
                        (item) => item.checked === false
                    );
                    break;
                case 'left':
                    this.itemsRight.forEach((item) => {
                        if (item.checked) {
                            this.itemsLeft.push({
                                name: item.name,
                                checked: false,
                            });
                        }
                    });
                    this.itemsRight = this.itemsRight.filter(
                        (item) => item.checked === false
                    );
                    break;
            }
        },
    },
};
</script>

<style>
.wrapper {
    display: flex;
}

.select-box {
    height: 100px;
    width: 150px;
    overflow-y: scroll;
    border: 1px solid black;
}

.buttons-wrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;
}
</style>
