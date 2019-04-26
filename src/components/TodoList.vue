<template>
    <el-row class="content">
        <el-col :xs="{span: 20, offset: 2}" :sm="{span: 8, offset: 8}">
            <span>
                欢迎: {{name}}! 你的待办事项是：
            </span>
            <el-input placeholder="请输入待办事项" v-model="todos" @keyup.enter.native="addTodos"></el-input>
            <el-tabs v-model="activeName">
                <el-tab-pane label="待办事项" name="first">
                    <el-col :xs="24">
                        <template v-if="!HasFinishAllTask">
                            <template v-for="(item, index) in list">
                                <div class="todo-list" v-if="item.status == false">

                                </div>
                            </template>
                        </template>
                        <template v-else-if="HasFinishAllTask">
                            暂无待办事项
                        </template>
                    </el-col>
                </el-tab-pane>
            </el-tabs>
        </el-col>
    </el-row>
</template>
<script>
import { truncate } from 'fs';
export default {
    data () {
        return {
            name: 'xbao',
            todos: '',
            activeName: 'first',
            list: [],
            count: 0
        };
    },
    computed: {
        HasFinishAllTask() {
            let count = 0;
            let length = this.list.length;
            for(let task of this.list) {
                this.list.status == true ? count += 1 : '';
            }
            this.count = count;
            if (this.count == length || length == 0) {
                return true;
            }else {
                return false;
            }
        }
    },
    methods: {
        addTodos() {
            if (this.todos == '') {
                return
            }else {
                let obj = {status: false, content: this.todos};
                this.list.push(obj);
                this.todos = '';
            }
        }
    }
}
</script>
<style lang="stylus" scoped>

</style>

