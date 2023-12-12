# GPU Nodes

## Overview <a href="#gpunodes-overview" id="gpunodes-overview"></a>

### Compute Resources <a href="#gpunodes-computeresources" id="gpunodes-computeresources"></a>

More detailed information on system resources can be found on our [Compute Resources page](https://uarizona.atlassian.net/wiki/spaces/UAHPC/pages/75990208/Compute+Resources).

### Containers with GPU Support <a href="#gpunodes-containerswithgpusupport" id="gpunodes-containerswithgpusupport"></a>

Singularity containers are available as modules on HPC for GPU-supported workflows. For more information, see our [documentation on Containers](https://uarizona.atlassian.net/wiki/spaces/UAHPC/pages/75990594/Containers).

### Accessing GPUs <a href="#gpunodes-accessinggpus" id="gpunodes-accessinggpus"></a>

Information on how to request GPUs using SLURM can be found in our [SLURM Documentation](https://uarizona.atlassian.net/wiki/spaces/UAHPC/pages/75989875/Running+Jobs+with+Slurm#RunningJobswithSlurm-GPUJobs).

### Training <a href="#gpunodes-training" id="gpunodes-training"></a>

For a list of training resources related to GPU workflows, see our [Training documentation](https://uarizona.atlassian.net/wiki/spaces/UAHPC/pages/75989137/Training#Training-GPU/NvidiaTraining).

***

## Cluster Information <a href="#gpunodes-clusterinformation" id="gpunodes-clusterinformation"></a>

<details>

<summary>Puma</summary>

Puma has a different arrangement for GPU nodes than Ocelote and ElGato. Whereas the older clusters have one GPU per node, Puma has four. This has a financial advantage for providing GPU's with lower overall cost, and a technical advantage of allowing jobs that can use multiple GPU's to run faster than spanning multiple nodes. This capability comes from using a newer operating system.\
Each node has four Nvidia V100S model GPUs. They are provisioned with 32GB memory compared to 16GB on the P100's.

<img src="../../.gitbook/assets/PUMA GPU image.jpg" alt="" data-size="original">

</details>

<details>

<summary>Ocelote</summary>

Ocelote has 46 compute nodes with Nvidia P100 GPUs that are available to researchers on campus. The limitation is a maximum of 10 concurrent jobs. Previously, one node with a V100 was available, but it has since been replaced with a P100. Tasks which require multiple GPUs must either request multiple nodes on Ocelote, or use Puma's GPU nodes.

<img src="../../.gitbook/assets/ocelote gpu image.png" alt="" data-size="original">



</details>

## Cuda Modules <a href="#gpunodes-cudamodules" id="gpunodes-cudamodules"></a>

_<mark style="color:red;">Nvidia Nsight Compute (the interactive kernel profiler) is not available. In response to a security alert (CVE-2018-6260) this capability is only available with root authority which users do not have.</mark>_&#x20;

The latest Cuda module available on the system is **11.0** and is the only version until newer ones come along. The Cuda driver version can be queried with the `nvidia-smi` command. To see the modules available, in an interactive session simply run:

```
$ module avail cuda
 
-------------------- /opt/ohpc/pub/moduledeps/gnu8-openmpi3 --------------------
   cp2k-cuda/7.1.0
 
-------------------------- /opt/ohpc/pub/modulefiles ---------------------------
   cuda11-dnn/8.0.2    cuda11-sdk/20.7    cuda11/11.0
```

## OpenACC <a href="#gpunodes-openacc" id="gpunodes-openacc"></a>

The OpenACC API is a collection of compiler directives and runtime routines that allow you to specify loops and regions of code in standard C, C++, and Fortran that you can offload from a host CPU to the GPU.

We provide two methods of support for OpenACC

1. We support OpenACC in the PGI Compiler.  The PGI implementation of OpenACC is considered the best implementation.  \
   "module load pgi" on Ocelote. If you are on a GPU node from an interactive session you can run "pgaccelinfo" to test functionality.  Remember that the login nodes do not have GPUs or software installed.  \
   A useful getting-started guide written by Nvidia is available here: [https://www.pgroup.com/doc/openacc17\_gs.pdf](https://www.pgroup.com/doc/openacc17\_gs.pdf) \

2. We support OpenACC in the GCC Compiler 6.1 which is automatically loaded as a module when you log into Ocelote.  Verify with "module list".\
   The GCC 6 release includes a much improved implementation of the OpenACC 2.0a specification.\
   A useful quick reference guide is available from: [https://gcc.gnu.org/wiki/OpenACC#Quick\_Reference\_Guide](https://gcc.gnu.org/wiki/OpenACC#Quick\_Reference\_Guide)

## Applications <a href="#gpunodes-applications" id="gpunodes-applications"></a>

Many applications have been optimized to run faster on GPU's. These include:

| Application                                                                            | Information                                                                                                                                                             | Access                       |
| -------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------- |
| ABAQUS                                                                                 | Installed as a module and available as an application through Open OnDemand                                                                                             | `$ module load abaqus`       |
| ANSYS Fluent                                                                           | Installed as a module and available as an application through Open OnDemand                                                                                             | `$ module load ansys`        |
| GAUSSIAN                                                                               | Installed as a module. [See these notes](https://uarizona.atlassian.net/wiki/spaces/UAHPC/pages/75993172/Gaussian+GPU+Notes).                                           | `$ module load gaussian/g16` |
| GROMACS                                                                                | Installed as a module                                                                                                                                                   | `$ module load gromacs`      |
| LAMMPS                                                                                 | Installed as a module                                                                                                                                                   | `$ module load lammps`       |
| [MATLAB](https://uarizona.atlassian.net/wiki/spaces/UAHPC/pages/75989586/Using+Matlab) | Installed as a module and available as an application through Open OnDemand. Review the GPU Coder on their [website](https://www.mathworks.com/products/gpu-coder.html) | `$ module load matlab`       |
| ML and DL Frameworks                                                                   | See the section below.                                                                                                                                                  | <p><br></p>                  |
| NAMD                                                                                   | Installed as a module                                                                                                                                                   | `$ module load namd`         |
| RELION                                                                                 | Available as a Singularity container or as a module.                                                                                                                    | `$ module load relion`       |
| VASP                                                                                   | A restricted license version is installed; only available to licensed users                                                                                             | `$ module load vasp`         |

### Python ML/DL including Nvidia RAPIDS  <a href="#gpunodes-pythonml-dlincludingnvidiarapids" id="gpunodes-pythonml-dlincludingnvidiarapids"></a>

The minimum version of Python that is supported is 3.6:

| Framework   | Details                                                                                         |
| ----------- | ----------------------------------------------------------------------------------------------- |
| caffe2      | A deep learning framework                                                                       |
| cudf        | RAPIDS: Cuda Dataframes supports loading and manipulating datasets                              |
| cuml        | RAPIDS: Cuda Machine Learning has many ML algorithms like K-means, PCA and SVM                  |
| numba       | RAPIDS: numba is for Cuda programming                                                           |
| tensorboard | Visualization tool for machine learning                                                         |
| tensorflow  | TensorFlow is an open source software library for numerical computation using data flow graphs. |
| tensorrt    | Inference server for deep learning                                                              |
| torch       | PyTorch supports tensor computation and deep neural networks                                    |

