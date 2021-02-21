<template>
    <el-dialog
    title="提示"
    :visible.sync="subdialogstate"
    width="30%"
    :before-close="handleClose">
    <div>
        <el-input v-model="batch" @change="handleChange1"></el-input>
        <el-input-number v-model="num" @change="handleChange" :min="1" :max="10" label="描述文字"></el-input-number> 
        <h6>{{items}}</h6>
        <sub_test v-for="(item,index) in items"
            :key="index"
            :index="index"
            :items="items"
            @deleteIndex="del"
            @uploadData="getData">
        </sub_test>
        <button @click="add">Add</button>  
    </div>        
    </el-dialog>
</template>



<script>
import sub_test from '@/components/sub_test.vue'
export default {
    data(){
        return{
            subdialogstate:false,
            num: 1,
            batch:0,
            items: [{}],
            dataRec: []
        }
    },
    props:['dialogstate'],
    components: {
        sub_test
    },
    watch: {
            dialogstate: function(newVal,oldVal){
                this.subdialogstate = newVal;  //newVal即是chartData
                // this.drawChart();
            }
    },
    methods:{
        // tosub(){this.data.subdialogstate=this.dialogstate},
        handleClose(done) {
            this.$confirm('确认关闭 ？')
            .then(_ => {
            done();
            this.$emit('closed');
            })
            .catch(_ => {});
            },
        handleChange(value) {
            this.batch=this.num*100
        },
        handleChange1(value) {
            this.num=Math.ceil(this.batch/100)
        },
        add: function () {
        this.items.push({name: '', age: ''})
        },
        // delete student
        del: function (index) {
        //  not allow to delete the first
        if (index !== 0) {
            this.items.splice(index, 1)
            console.log('deleted:', JSON.stringify(this.items))
        }
        },
        //  get the data from child
        getData: function (val) {
        let index = val.index
        this.items[index] = val.data
        }

    }

}
</script>