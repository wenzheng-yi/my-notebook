根据文档里边模块及function方法的顺序进行阅读

- useActiveElement

````typescript
export function useActiveElement<T extends HTMLElement>(options: ConfigurableWindow = {}) {
  const { window = defaultWindow } = options
  const counter = ref(0)

  if (window) {
    useEventListener(window, 'blur', () => counter.value += 1, true)
    useEventListener(window, 'focus', () => counter.value += 1, true)
  }

  return computed(() => {
    counter.value
    return window?.document.activeElement as T | null | undefined
  })
}
````

方法注解：

1、方法中利用了一个counter变量，把window的blur事件和focus事件集中起来，然后在computed中把counter作为依赖之一，通过counter的变化，触发computed中方法的执行，从而不断地返回最新的document.activeElement。

2、可传入选项式参数window，即可用于监听iframe中的window。

配套的还有组件形式的用法，其实就是在组件内部使用了useActiveElement方法，然后返回一个不带任何标签的纯文本。

````javascript
export const UseActiveElement = defineComponent({
  name: 'UseActiveElement',
  setup(props, { slots }) {
    const data = reactive({
      element: useActiveElement(),
    })

    return () => {
      if (slots.default)
        return slots.default(data)
    }
  },
})
````



