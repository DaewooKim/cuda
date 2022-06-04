# CUDA Thread Hiearchy
## Thread
* Basic Processing Unit
## Warp
* 32 Threads
* Basic execution unit
* Controlled by the same instructions
## Block
* Group of threads
* Threads in a block have different thread IDs
    + threadIdx (built-in variable)
* Can be 1D, 2D or 3D
* Grid는 많은 thread block으로 구성되어 있음
* thread block 내의 thread는 block-local synchronization, block-local share memory를 이용하여 협력함
* 서로 다른 block의 threads들은 서로 협력할 수 없음
## Grid
* Group of blocks
* Blocks in a grid have different block IDs
    + blockIdx
* Single kernel launch에 의해 생성된 모든 threads를 Grid라고 함
* Grid 안의 모든 thread는 동일한 Global Memory Space를 공유함
## Compute Capability (GPU의 능력)
* [Compute Copability] (https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#compute-capabilities)
* Max. Dim. of thread block : 3
* Max. x- or y-dim. of a block : 1024
* Max. z-dim of a block: 64
* Max. number of threads per block: 1024
* Warp: 32

# Grid & Block 인덱싱을 위한 built-in variables: 
## coordinate variables
* blockIdx (block index within a grid)
    * Grid 안에서 자신이 속한 block의 ID
    * blockIdx.x, blockIdx.y, blockIdx.z
* threadIdx (thread index within a block)
    * Block 안에서 자신의 thread ID
    * threadIdx.x, threadIdx.y, threadIdx.z
## Grid & Block Dim.
* blockDim (block dimension, measured in threads)
    * Block 안의 thread 수 결정
    * blockDim.x, blockDim.y, blockDim.z
* gridDim(grid dimension, measured in blocks)
    * Grid 안의 block 수 결정
    * gridDim.x, gridDim.y, gridDim.z

## Grid 와 Block Dim. 결정하기
* block size 결정
* 애플리케이션 데이터 사이즈와 block 사이즈에 기반하여 grid dim.을 계산
* block dim. 결정을 위해 고려해야할 것들
    * 커널의 성능 특성
    * GPU 리소스 제한

# SIMT(Single Instruction Multiple Threads)
* Thread들을 그룹 단위로 관리/실행
    * 예) 32 threads = Warp
* 모든 thread가 같은 프로그램 코드를 공유 → Kernel
* 각각의 thread가 자신만의 register state를 가짐
    * Instruction Address Counter 포함
    * 서로 독립적 수행이 가능함
* SIMD vs SIMT
    * SIMD는 하나의 instruction을 여러 개의 data에 적용
