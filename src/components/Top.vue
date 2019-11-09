<template id="top">
    <div>
        <header class="bar bar-nav">
            <a class="icon icon-left pull-left"></a>
            <a class="icon icon-edit pull-right" @click= "changeInputFlag"></a>
            <h1 class="title">todolist</h1>
        </header>
    </div> 
</template>


<script>
export default {
    methods: {
        changeInputFlag() {
            this.$emit('change-input-flag')
        }
    }
}
</script>