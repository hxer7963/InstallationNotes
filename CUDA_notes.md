* conceptual understanding of the CUDA memory model.
* CUDA thread execution model;
* GPU hardware performance features;
* modern computer system architecture;



* data-parallel programming patterns

算力为应用软件提供更多功能，如果只编写串行程序，我们只能依靠硬件的精度来提升程序的执行速度，随着功耗和散热问题，导致单处理器的速度提升受限，导致原先想依靠处理器升级换代而带来串行程序执行速度质的飞跃的期望破灭了。如果单个程序执行速度得不到提升，应用程序开发者将不能为软件提供新的特性和功能，整个计算机产业将会停滞(reduce the growth opportunities).

Q: 什么是超线程？two hardware threads?

并行计算的两种架构

* 多核CPUs：Intel Core i7多核处理器通常有4个处理器核，每个乱序执行，多指令发起，支持超线程，最大限度地提高串行程序的执行；
* 多线程(mang-thread) GPUs：专注于并行应用程序的执行吞吐量；随着处理器的迭代更新，支持的线程数越来越多；Nvidia GTX680 GPU支持16,384线程，以一种**简单、有序**的方式执行(simple、in-order pipelines)。

Q：为何多线程GPUs和通用多核CPUs的peak-performance gap在12年就相差10+倍？

硬件性能的对比实则考虑的是硬件的设计理念；

Multicore CPUs：·