<template>
  <div id="app">
   <!-- 布局外壳 layout -->
        <div class="page-group">
            <div class="page page-current fhc_page">
                <Top @change-input-flag="changeInputFlag"></Top>
                <input @keyup.13="addItem" class="fhc_input" v-show="inputFlag" type="text" v-model="inputVal">
                <Middle :todos="newTodos" @changeflag="changeFlag" @check="check"></Middle>
                <TabBar @changetype="changeType" :tabbars="tabbars" :type="type"></TabBar>
                <MaskComp v-show="maskFlag" @click.native="closeMask" @remove="remove" :active-index="activeIndex"></MaskComp>
            </div>
        </div>
  </div>
</template>

<script>

import Top from './components/Top.vue'
import Middle from './components/Middle.vue'
import TabBar from './components/TabBar.vue'
import MaskComp from './components/MaskComp.vue'

export default {
  name: 'app',
  components: { 
    Top,
    Middle,
    TabBar,
    MaskComp
  },
  data(){
    return{
       todos: [{
                id: 1,
                task: '事件1',
                flag: true
            }, {
                id: 2,
                task: '事件2',
                flag: true
            }

        ],
        tabbars: [{
                id: 1,
                text: 'A',
                class_name: 'all'
            },
            {
                id: 2,
                text: 'F',
                class_name: 'finish'
            }, {
                id: 3,
                text: 'U',
                class_name: 'unfinish'
            }
        ],
        type: 'A',
        inputFlag: false,
        inputVal: '',
        maskFlag: false,
        activeIndex: 0 //用于保存check后的index值 用于删除
        }
  },
  methods: {
        changeType(val) {
            this.type = val
        },
        changeFlag(index) {
            this.todos[index].flag = !this.todos[index].flag
        },
        check(index) {

            //在点击删除前  先判断一下当前数据的flag 是true 还是false
            if (this.todos[index].flag) {
                //直接删除
                this.remove(index)
            } else {
                this.activeIndex = index
                    //不能直接删除 弹出遮罩  mask
                this.maskFlag = true
            }
        },
        remove(index) {
            //pop shift splice
            this.todos.splice(index, 1)
        },
        changeInputFlag() {
            this.inputFlag = !this.inputFlag
        },
        addItem() {
            this.todos.push({
                id: this.todos.length + 1, //安全性极差
                task: this.inputVal,
                flag: true
            })
            this.inputVal = ""
            this.inputFlag = false
        },
        closeMask() {
            this.maskFlag = false
        },

    },
    computed: {
        newTodos() {
            switch (this.type) {
                case "A":
                    return this.todos
                    break;
                case "F":
                    return this.todos.filter(item => item.flag)
                case "U":
                    return this.todos.filter(item => !item.flag)
                    break;
                default:
                    break;
            }
        }
    }
}
</script>
<style lang="stylus" scoped>
.fhc_page {
    display: flex !important;
    flex-direction: column;
}
.fhc_input {
    margin-top: 50px;
    padding: 8px 10px;
}

</style>

<style lang="stylus" >
* {
    margin: 0;
    padding: 0;
    list-style: none;
}
</style>
