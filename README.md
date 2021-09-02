# Vue 生命周期

## v-if 指令对组件生命周期的影响

1. `v-if` 从 `false` 变为 `true`，会触发组件的 `beforeCreate`、`created`、`beforeMount` 和 `mounted` 钩子函数。
2. `v-if` 从 `true` 变为 `false`，会触发组件的 `beforeDestory` 和 `destoryed` 钩子函数。

## props 状态更新对组件的影响

[单向数据流](https://cn.vuejs.org/v2/guide/components-props.html#%E5%8D%95%E5%90%91%E6%95%B0%E6%8D%AE%E6%B5%81)

｜ 每次父级组件发生变更时，子组件中所有的 prop 都将会刷新为最新的值。这意味着你不应该在一个子组件内部改变 prop。

如果在 A 组件中定义了一个 prop 状态，而没有在做任何绑定使用，则当父组件中更新此状态时，A 组件的 `beforeUpdate` 和 `updated` 钩子函数不会被触发。
