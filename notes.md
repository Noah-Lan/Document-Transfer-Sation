##### TensorRT 和 Triton 的区别

+ 如果是要将模型和推理嵌入在服务或软硬件中，那么 TensorRT 是很好的选择，使用它来加载模型进行推理，提升性能 (TensorRT Runtime)

+ 不然，常规的做法是模型推理和其他业务隔离，模型统一部署在 Triton Server，然后其他业务通过 Triton Client 来进行模型推理的请求



##### 参数 `ctx/self`

+ `ctx` 是 context 的缩写，翻译成”上下文/环境“
+ `ctx` 专门用在静态方法中
+ `self` 指的是实例在静态方法中没有意义
+ 自定义的 `forward()` 方法和 `backward()` 方法第一个参数必须是 `ctx` 



##### 计算图导出方法

+ 跟踪 `torch.jit.trace`
  + 只能通过实际运行一遍模型的方法导出模型静态图，即无法识别出模型中的控制流（如循环）
+ 记录 `torch.jit.script`
  + 能通过解析模型来正确记录所有的控制流

![img](https://pic3.zhimg.com/80/v2-ebee8fc8a37570c8a2e7b05596104b06_1440w.webp)

