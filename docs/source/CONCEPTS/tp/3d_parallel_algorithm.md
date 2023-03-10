# 3D parallel Algorithm

* Paper: [https://arxiv.org/pdf/2105.14450.pdf](https://arxiv.org/pdf/2105.14450.pdf)

![E4D02BEB-A5BB-461D-9B62-213A61DB5B74.jpeg](3d_image/E4D02BEB-A5BB-461D-9B62-213A61DB5B74.jpeg)

1D, 2D, and 2.5D, which have been previously proposed to address the challenges posed by large models. 1D tensor parallelism involves splitting the tensor along one dimension, while 2D tensor parallelism splits the tensor into rows and columns, reducing memory cost but introducing more communication. A 2.5D tensor parallelism algorithm has also been proposed based on the 2.5D SUMMA to reduce communication by using more devices. This algorithm involves splitting the input tensor into multiple layers and the weight tensor into multiple sub-tensors. Finally, the paper proposes a 3D model parallelism technique to further harness the capability of GPU clusters. This technique divides both computation and memory of a single neural network among multiple GPUs in three dimensions, and is designed to address the limitations of 2D tensor parallelism.

## Usage

Using `ParallelMode.TENSOR_1D` as a parameter of `tensor_parallel_mode`. 

`tp_size` is must be **2^n of natural number.**

Also, you should `tp_depth` to **1.**(tp_depth only used in 2.5d)

```python
# model = defined in section 2.2

tp_size = 8
tp_depth = 1

parallel_context = ParallelContext.from_torch(
    data_parallel_size=1,
    pipeline_parallel_size=1,
    tensor_parallel_size=tp_size,
    tensor_parallel_mode=ParallelMode.TENSOR_3D,
    tensor_parallel_depth=tp_depth,
)
oslo.ready(model, parallel_context)
```