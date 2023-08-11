# vue-okr-tree
基于vue2 关系图,关系网,思维导图
---
title: 2.vue-okr-tree使用
date: 2023/05/29
---
## 2.vue-okr-tree 使用报错解决办法
## 前言 

vue-okr-tree使用遇到报错问题解决办法。

```

1.  我从`vue-okr-tree`把组件单独提取出来使用,不经过`npm`安装,使用步骤如下。
2.  在  `github`仓库`clone`或`下载`会得到`vue-okr-tree`文件夹,放到`src/components`目录下。

```
[github][]
[github]: https://github.com/kuikui2/vue-okr-tree.git

> 例子
```vue
<template>
	<div>
		<vue-okr-tree :data="testData"></vue-okr-tree> 
		
	</div>
</template>

<script>
		// 组件放 components目录比较合适,也可自行更换目录.
		import { VueOkrTree } from '@/components/vue-okr-tree';
  export default {
	  // 注册组件
	  components: {
	     VueOkrTree
	   },
    data () {
      return {
        testData: [{
          label: 'xxx科技有有限公司',
          children: [{
            label: '产品研发部',
            children: [{
              label: '研发-前端',
            }, {
              label: '研发-后端',
            }, {
              label: 'UI 设计',
            }]
          }, {
            label: '销售部',
            children: [{
                label: '销售一部',
              },{
                label: '销售二部',
              }
            ]
          },{
            label: '财务部'
          }]
        }]
      }
    }
  }
</script>
```
## 分析 

 *  既然是树，那么每个节点都应该是相同的组件
 *  节点下面套节点，所以节点组件应该是一个递归组件
 *  整棵树应该有一个全局的状态，用来管理从外部传入的值以及向外部提供的属性和方法。
 *  每相树节点应该也要有一个对应的节点状态，来管理节点自身属性和方法。

## 下方是vue-okr-tree文档,可直接使用

#### [vue-okr-tree官方文档][] 
[vue-okr-tree官方文档]: http://www.longstudy.club/vue-okr-tree-doc/index.html

#### 基础用法 

基础的树形结构展示，默认方式垂直方向。

![pic_157b567f.png](https://124.70.33.149:9998/images/pic_157b567f.png)

#### 水平方向 

将 `direction` 属性设置为 `horizontal` 就可以展示水平方向。

![pic_45de68de.png](https://124.70.33.149:9998/images/pic_45de68de.png)

#### 节点是否可被展开 

节点可被展开,默认是不展开，通过`show-collapsable`设置节点可被展开。

![pic_2f9456e6.png](https://124.70.33.149:9998/images/pic_2f9456e6.png)

#### 节点默认全部展开 

通过设置 `default-expand-all` 默认展开所有节点，该参数只有在 `show-collapsable` 为`true` 时有效

![pic_8796fff5.png](https://124.70.33.149:9998/images/pic_8796fff5.png)

#### 可将 Tree 的某些节点设置为默认展开 

![pic_34cc2fd7.png](https://124.70.33.149:9998/images/pic_34cc2fd7.png)

通过 `default-expanded-keys` 设置默认展开的节点。需要注意的是，此时必须设置 `node-key` ，其值为节点数据中的一个字段名，该字段在整棵树中是唯一的。

## 节点的样式 

可自行设置节点的默认样式和选中的样式。

通过 `label-class-name` 设置节点的样式，支持字符和函数方式。通过 `current-lable-class-name` 设置当前节点选中的样式，支持字符和函数方式。

![pic_2b34a177.png](https://124.70.33.149:9998/images/pic_2b34a177.png)

#### 节点自定义内容 

可自行设置节点内容。通过 `render-content` 渲染节点内容。

![pic_30707488.png](https://124.70.33.149:9998/images/pic_30707488.png)

#### OKR 展示模式 

该模式的出现，是为了实现跟飞书OKR 展示的视图一样效果，所以在 Tree 的模式下，扩展成左右两棵子树。  
该模式必须设置 `onlyBothTree` ，以及通过 `leftData`表示左子数的结构。

![pic_a477f19d.png](https://124.70.33.149:9998/images/pic_a477f19d.png)

#### OKR 展示模式之自定义节点内容 

与上常规 Tree 一样，我们也可以通过自定义渲染函数来制定节点的内容。

通过 `render-content` 渲染节点内容，通过返回 node 中的 `isLeftChild` 判断是否是左边的树。

![pic_d7747c63.png](https://124.70.33.149:9998/images/pic_d7747c63.png)

#### 节点过滤(不可展开)及支持的方法 

通过关键字过滤树节点，在需要对节点进行过滤时，调用 Tree 实例的 filter 方法，参数为关键字。需要注意的是，此时需要设置 `filter-node-method` ，值为过滤函数。

![pic_decc26fb.png](https://124.70.33.149:9998/images/pic_decc26fb.png)

#### 节点过滤(可被展开) 

通过关键字过滤树节点，在需要对节点进行过滤时，调用 Tree 实例的 `filter` 方法，参数为关键字。需要注意的是，此时需要设置 `filter-node-method` ，值为过滤函数。

![pic_3cc1f833.png](https://124.70.33.149:9998/images/pic_3cc1f833.png)

#### 支持的事件(不可展开) 

不可展开时支持的事件有 节点点击 和 鼠标右键点击。

![pic_b9a92345.png](https://124.70.33.149:9998/images/pic_b9a92345.png)

#### 支持的事件(可被展开) 

可展开时支持的事件有 节点点击、鼠标右键点击，节点的展开以及节点的关闭。

![pic_c7b1ea03.png](https://124.70.33.149:9998/images/pic_c7b1ea03.png)

## Attributes 

<table> 
 <thead> 
  <tr> 
   <th>参数</th> 
   <th>说明</th> 
   <th>类型</th> 
   <th>可选值</th> 
   <th>默认值</th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td>data</td> 
   <td>展示数据</td> 
   <td>array</td> 
   <td>—</td> 
   <td>—</td> 
  </tr> 
  <tr> 
   <td>direction</td> 
   <td>树的展开方向</td> 
   <td>String</td> 
   <td>horizontal / vertical</td> 
   <td>vertical</td> 
  </tr> 
  <tr> 
   <td>onlyBothTree</td> 
   <td>子树在根节点左右两边展开，该模式只有在 direction 为 horizontal 有效，且必须提供 leftData 数据</td> 
   <td>Boolean</td> 
   <td>—</td> 
   <td>false</td> 
  </tr> 
  <tr> 
   <td>leftData</td> 
   <td>展示左子数的数据，该属性于在 onlyBothTree 模式启用</td> 
   <td>array</td> 
   <td>—</td> 
   <td>—</td> 
  </tr> 
  <tr> 
   <td>label-width</td> 
   <td>节点的宽度，默认为自动宽度。如果 label-width 为 number 类型，单位 px；如果 label-width 为 string 类型，则这个宽度会设置为 节点 的 style.width 的值，节点的宽度会受控于外部样式</td> 
   <td>string/number</td> 
   <td>—</td> 
   <td>—</td> 
  </tr> 
  <tr> 
   <td>label-height</td> 
   <td>节点的高度，默认为自动高度。如果 label-height 为 number 类型，单位 px；如果 label-height 为 string 类型，则这个高度会设置为 节点 的 style.height 的值，节点的高度会受控于外部样式</td> 
   <td>string/number</td> 
   <td>—</td> 
   <td>—</td> 
  </tr> 
  <tr> 
   <td>label-class-name</td> 
   <td>节点 className 的回调方法，也可以使用字符串为所有的节点设置一个固定的 className</td> 
   <td>Function(node)/String</td> 
   <td>—</td> 
   <td>—</td> 
  </tr> 
  <tr> 
   <td>current-lable-class-name</td> 
   <td>当前选中节点的样式</td> 
   <td>Function(node)/String</td> 
   <td>—</td> 
   <td>—</td> 
  </tr> 
  <tr> 
   <td>show-collapsable</td> 
   <td>节点是否可被展开</td> 
   <td>Boolean</td> 
   <td>—</td> 
   <td>false</td> 
  </tr> 
  <tr> 
   <td>default-expand-all</td> 
   <td>是否默认展开所有节点，该参数只有在 show-collapsable 为 true 时有效</td> 
   <td>Boolean</td> 
   <td>—</td> 
   <td>false</td> 
  </tr> 
  <tr> 
   <td>render-content</td> 
   <td>树节点的内容区的渲染 Function</td> 
   <td>Function(h, node)</td> 
   <td>—</td> 
   <td>—</td> 
  </tr> 
  <tr> 
   <td>props</td> 
   <td>配置选项，具体看下表</td> 
   <td>object</td> 
   <td>—</td> 
   <td>—</td> 
  </tr> 
  <tr> 
   <td>node-key</td> 
   <td>每个树节点用来作为唯一标识的属性，整棵树应该是唯一的</td> 
   <td>String</td> 
   <td>—</td> 
   <td>—</td> 
  </tr> 
  <tr> 
   <td>default-expanded-keys</td> 
   <td>默认展开的节点的 key 的数组(需要注意的是，此时必须设置node-key，其值为节点数据中的一个字段名，该字段在整棵树中是唯一的。)</td> 
   <td>array</td> 
   <td>—</td> 
   <td>—</td> 
  </tr> 
  <tr> 
   <td>filter-node-method</td> 
   <td>对树节点进行筛选时执行的方法，返回 true 表示这个节点可以显示，返回 false 则表示这个节点会被隐藏</td> 
   <td>Function(value, data, node)</td> 
   <td>—</td> 
   <td>—</td> 
  </tr> 
 </tbody> 
</table>

## props 

<table> 
 <thead> 
  <tr> 
   <th>参数</th> 
   <th>说明</th> 
   <th>类型</th> 
   <th>可选值</th> 
   <th>默认值</th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td>label</td> 
   <td>指定节点标签为节点对象的某个属性值</td> 
   <td>string, function(data, node)</td> 
   <td>—</td> 
   <td>—</td> 
  </tr> 
  <tr> 
   <td>children</td> 
   <td>指定节点标签为节点对象的某个属性值</td> 
   <td>string</td> 
   <td>—</td> 
   <td>—</td> 
  </tr> 
 </tbody> 
</table>

## \#\# Events 

<table> 
 <thead> 
  <tr> 
   <th>事件名称</th> 
   <th>说明</th> 
   <th>回调参数</th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td>node-click</td> 
   <td>节点被点击时的回调</td> 
   <td>共三个参数，依次为：传递给 data 属性的数组中该节点所对应的对象、节点对应的 Node、节点组件本身。</td> 
  </tr> 
  <tr> 
   <td>node-expand</td> 
   <td>节点被展开时触发的事件</td> 
   <td>共三个参数，依次为：传递给 data 属性的数组中该节点所对应的对象、节点对应的 Node、节点组件本身</td> 
  </tr> 
  <tr> 
   <td>node-collapse</td> 
   <td>节点被关闭时触发的事件</td> 
   <td>共三个参数，依次为：传递给 data 属性的数组中该节点所对应的对象、节点对应的 Node、节点组件本身</td> 
  </tr> 
  <tr> 
   <td>node-contextmenu</td> 
   <td>当某一节点被鼠标右键点击时会触发该事件</td> 
   <td>共四个参数，依次为：event、传递给 data 属性的数组中该节点所对应的对象、节点对应的 Node、节点组件本身。</td> 
  </tr> 
 </tbody> 
</table>

## 方法 

<table> 
 <thead> 
  <tr> 
   <th>方法名</th> 
   <th>说明</th> 
   <th>回调参数</th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td>filter</td> 
   <td>对树节点进行筛选操作</td> 
   <td>接收一个任意类型的参数，该参数会在 filter-node-method 中作为第一个参数</td> 
  </tr> 
  <tr> 
   <td>getNode</td> 
   <td>根据 data 或者 key 拿到 Tree 组件中的 node,使用此方法必须设置 node-key 属性</td> 
   <td>(data) 要获得 node 的 key 或者 data</td> 
  </tr> 
  <tr> 
   <td>setCurrentNode</td> 
   <td>通过 node 设置某个节点的当前选中状态，使用此方法必须设置 node-key 属性</td> 
   <td>(node) 待被选节点的 node</td> 
  </tr> 
  <tr> 
   <td>setCurrentKey</td> 
   <td>通过 key 设置某个节点的当前选中状态，使用此方法必须设置 node-key 属性</td> 
   <td>(key) 待被选节点的 key，若为 null 则取消当前高亮的节点</td> 
  </tr> 
  <tr> 
   <td>getCurrentKey</td> 
   <td>获取当前被选中节点的 key，使用此方法必须设置 node-key 属性，若没有节点被选中则返回 null</td> 
   <td>—</td> 
  </tr> 
  <tr> 
   <td>getCurrentNode</td> 
   <td>获取当前被选中节点的 data，若没有节点被选中则返回 null</td> 
   <td>—</td> 
  </tr> 
  <tr> 
   <td>remove</td> 
   <td>删除 Tree 中的一个节点，使用此方法必须设置 node-key 属性</td> 
   <td>(data) 要删除的节点的 id 或者 data 或者 node</td> 
  </tr> 
  <tr> 
   <td>append</td> 
   <td>为 Tree 中的一个节点追加一个子节点</td> 
   <td>(data, parentNode) 接收两个参数，1. 要追加的子节点的 data 2. 子节点的 parent 的 data、key 或者 node</td> 
  </tr> 
  <tr> 
   <td>insertBefore</td> 
   <td>为 Tree 的一个节点的前面增加一个节点</td> 
   <td>(data, refNode) 接收两个参数，1. 要增加的节点的 data 2. 要增加的节点的后一个节点的 data、key 或者 node</td> 
  </tr> 
  <tr> 
   <td>insertAfter</td> 
   <td>为 Tree 的一个节点的后面增加一个节点</td> 
   <td>(data, refNode) 接收两个参数，1. 要增加的节点的 data 2. 要增加的节点的前一个节点的 data、key 或者 node</td> 
  </tr> 
 </tbody> 
</table>



[Vue]: https://cn.vuejs.org/v2/guide/components-edge-
