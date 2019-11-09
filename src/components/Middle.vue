<template id="middle">
    <div class="fhc_content">
        <div class="card"
        v-for = "(item,index) in todos" :key="item.id"
        >
            <div class="card-content">
                <div class="card-content-inner">
                    <p> {{item.task}}</p>
                    <div class="fhc_btn_box pull-right">
                            <button class="button "
                            :class = " {'button-fill':item.flag} "
                            @click = "changeflag(index)"
                            >
                                <i class="icon icon-check"></i>
                            </button>
                            <button class="button button-danger"
                            @click = "removeItem(index)"
                            >
                                <i class="icon icon-remove"></i>
                            </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="stylus" scoped>
.fhc_content {
    padding-top: 40px;
    flex: 1;
}
.fhc_btn_box {
    display: flex;
}
.card-content-inner {
    overflow: hidden;
}
.fhc_btn_box button {
    margin-right: 10px;
}
</style>

<script>
export default {
     props: ['todos'],
    methods: {
        changeflag(index) {
            this.$emit('changeflag', index)
        },
        removeItem(index) {
            this.$emit('check', index)
        }
    }
}
</script>