<template>
<div class="wrapper">
  <div class="box">
    <div v-for="item in items" :key="item.id">
      <input type="checkbox" :value="item.id">
        {{ item.name }}
      </input>
    </div>
  </div>

  <div class="buttons-wrapper">
    <button type="button"> -> </button>
    <button type="button"> <- </button>
  </div>

  <div class="box">
    <div v-for="item in transferedItems" :key="item.id">
      <input type="checkbox" :value="item.id">
        {{ item.name }}
      </input>
    </div>
  </div> 
</div>

</template>

<script>
export default {
  name: 'TransferComponent',

  data() {
    return {
      transferedItems: [],
      items: [
        {
          id: 0,
          name: 'Max',
        },
        {
          id: 1,
          name: 'Luuk',
        },
        {
          id: 2,
          name: 'Shaldi',
        },
        {
          id: 3,
          name: 'Arie',
        },
        {
          id: 4,
          name: 'Tobias',
        },
        {
          id: 5,
          name: 'Sjors',
        },
      ],
    };
  },
};
</script>

<style>
.wrapper {
  display: flex;
}

.box {
  border: 1px solid black;
  min-width: 150px;
  /* margin-right: 2rem; */
}

.buttons-wrapper {
  
}
</style>
