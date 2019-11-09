<template id="tabbar">
    <div>
    <footer>
        <ul class="fhc_list">
            <li class="circle" @click="change(item.text)"  v-for = 'item in tabbars' :key='item.id' :class="['circle-' + item.class_name ,type ===item.text &&'circle-fill'  ]"> {{item.text}} </li>
        </ul>
    </footer>
    </div>
</template>

<style lang="stylus" scoped>
.fhc_list {
    display: flex;
    justify-content: space-around;
  
}
.circle {
    width: 80px;
    height: 80px;
    border: 1px solid #ccc;
    border-radius: 50%;
    text-align: center;
    line-height: 80px;
}

.circle.circle-all {
    border-color: green;
    color: green;
}

.circle.circle-all.circle-fill {
    background: green;
    color: white;
}

.circle.circle-finish {
    border-color: blue;
    color: blue;
}

.circle.circle-finish.circle-fill {
    background: blue;
    color: white;
}

.circle.circle-unfinish {
    border-color: red;
    color: red;
}

.circle.circle-unfinish.circle-fill {
    background: red;
    color: white;
}
</style>

<script>
export default {
    props: ['tabbars', 'type'],
    methods: {
        change(val) {
            this.$emit('changetype', val)
        }
    }
}
</script>