<template>
    <div @click="handleClick" :class="[
        'grid place-items-center w-40 h-40',
        index < 3 ? 'border-b-[#E3E6E8] border-b-solid border-b-2' : '',
        index > 5 ? 'border-t-[#E3E6E8] border-t-solid border-t-2' : '',
        index === 0 || index === 3 || index === 6 ? 'border-r-[#E3E6E8] border-r-solid border-r-2' : '',
        index === 2 || index === 5 || index === 8 ? 'border-l-[#E3E6E8] border-l-solid border-l-2' : ''
    ]">
        <slot></slot>
    </div>
</template>
  
<script>
export default {
    props: {
        index: Number,
        updateBoard: Function
    },
    methods: {
        handleClick() {
            this.updateBoard(this.index, false);
        }
    }
};
</script>
  