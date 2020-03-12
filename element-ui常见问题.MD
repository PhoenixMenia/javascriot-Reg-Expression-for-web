# element-ui常见的坑

### element用v-for循环出来的表单验证

1.修改prop值

主要是prop值，prop中的第一个值要为遍历数据中的picPlayJson,中间拼接索引，然后拼接v-model中的值，如下例子所示：

2.单独为当前数据添加表单验证

```
// html
// :prop="'other.' + index + '.otherCharges'"    注意这个小数点一定不能楼掉，漏掉就会报错

<el-form :model="model" ref="settingForm">
  <div class="dragger-list">
    <draggable v-model="model.picPlayJson" @update="datadragEnd">
      <transition-group>
        <div class="drag-img-item" v-for="(item, index) in model.picPlayJson" :key="index">
          <img :src="item.imgUrl">
          <el-form-item class="vr-form-address" :prop="'picPlayJson.' + index + '.desc'" :rules="desc">
            <el-input v-model="item.desc" resize="none" placeholder="图片描述"></el-input>
          </el-form-item>
          <i class="close-icon el-icon-circle-close" @click.prevent.stop="handleRemove(index)"></i>
        </div>
      </transition-group>
    </draggable>
  </div>
</el-form>

```

```
// js 要注意的就是表单验证的rules要写在当前验证的那个<el-form-item>内，否则无法生效

<script>
  export default {
    data () {
      return {
        model: {
          picPlayJson: []
        },
        desc: [
          { min: 0, max: 10, message: '不能超过10个字符', trigger: ['blur', 'change'] }
        ]
      };
    }
  };
</script>
```


