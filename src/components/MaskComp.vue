<template id="maskcomp">
    <div class="mask-box">
        <div class="mask-bg">
            <div class="mask-content">
                <p>您确定要删除吗？</p>
                <button class="button button-fill button-warning pull-right"
                @click = "removeItem(activeIndex)"
                >确定</button>
            </div>
        </div>
    </div>

</template>

<style lang="stylus" scoped>
.mask-box {
    position: fixed;
    left: 0;
    top: 0;
    z-index: 100;
    width: 100%;
    height: 100%;
}

.mask-bg {
    position: absolute;
    left: 0;
    top: 0;
    background: rgba(0, 0, 0, .5);
    width: 100%;
    height: 100%;
}

.mask-content {
    position: absolute;
    margin: auto;
    left: 0;
    top: 0;
    bottom: 0;
    right: 0;
    width: 80%;
    padding: 15px;
    height: 100px;
    background: #fff;
    border-radius: 10px;
    overflow: hidden;
}

.mask-content p {
    margin: 0;
    margin-bottom: 10px;
}
</style>

<script>
export default {
     template: '#maskcomp',
    methods: {
        removeItem(index) {
            this.$emit('remove', index)
        }
    },
    props: ['activeIndex']
}
</script>