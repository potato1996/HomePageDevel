# CUDA - Tips&Tricks

This page contains some general tips&tricks when writing CUDA kernels, as well as list some possible ideas when optimize our kernels

## General Tips&Tricks

1. Registers are NOT index-able. That's why sometimes small array will be spilled into local memory

2. When unrolling template variables, e.g `template<int K>`, use `#pragma unroll(K)` instead of `#pragma unroll` when you would like to gurante to unroll the whole loop.

3. Continue on 2: you can use other numbers to achieve a different level of unrolling, which would possiblly help on saving some registers

4. when profiling (like checking assembly, etc.), use `-lineinfo` instead of `-G`, the later one will disable most of compiler optimizations...

5. GPU do NOT have a branch prediction...by default, but we can manually insert `WAIT.1` in assembly

6. On Volta architecture, we cannot assume that the threads within a warp is always synced - as long as we have divergence. use `__syncwarp()` to sync them

## What to do if latency bound?

## What to do if memory bandwidth bound?

## What to do if computation bound?


