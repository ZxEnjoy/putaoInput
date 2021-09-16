1.随着组件输入内容的增加，组件的宽度和高度可以自动扩展，宽度扩展到和组件父容器宽度相同的时候，进行高度的扩展。

![enter](https://github.com/ZxEnjoy/putaoInput/blob/main/gif/oherline.gif)

2.支持换行符的输入。

![enter](https://github.com/ZxEnjoy/putaoInput/blob/main/gif/enter.gif)

3.maxlength属性演示

![maxlength](https://github.com/ZxEnjoy/putaoInput/blob/main/gif/maxlength.gif)

4.disabled属性演示![disabled](https://github.com/ZxEnjoy/putaoInput/blob/main/gif/disabled.gif)

5.placeholder属性演示![placeholder](https://github.com/ZxEnjoy/putaoInput/blob/main/gif/placeholder.gif)

> 使用方法：
```
import xinput from './components/Input'
<xinput ></xinput>
```
> 说明

| 属性        | 描述               | 类型    | 默认值 |
| ----------- | ------------------ | ------- | ------ |
| placeholder | 期值的提示信息     | String  | ---    |
| maxlength   | 输入文本的最大长度 | Number  | ---    |
| disabled    | 是否可编辑         | String  | ---    |
| min_width   | 组件最小宽度       | Number  | 300    |
| value       | 文本值             | v-model | ---    |

