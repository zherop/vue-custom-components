# vue-custom-components
基于vue，Element-UI自定义常用组件

# 组件列表

## JsonEditor

	依赖vue-codemirror，支持Json数据的友好展示，以及粘贴时，自动格式化显示，简单易用。

#### 基本用法
```
<json-editor v-model="jsonData"></json-editor>
```

#### Attributes

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| ------ | ------ | ------ | ------ | ------ |
| value | 绑定值 | string / object | - | - |
