# CMSC818J Assignment 2- GraphBIG Benchmark

This is a collection of benchmarks that could be used to complete Assignment 2. The name of the benchmark is GraphBIG, and it tests a variety of workloads for graph computing. The workloads are selected from real-world use cases of IBM System G customers.

## Logging into Junkfood
This benchmark requires access to a linux environment that can execute perf. The officially supported environment is junkfood. If you have access
to hardware running linux that has perf, you can use it, but the TA may be unable to help you. Use at your own risk.

:warning: **You must login to a specific junkfood host for perf to work**. The junkfood server is made up of three hosts: two physical servers (krispykreme and cheezit) and a VM (biggulp). Logging on using `ssh <username>@junkfood.cs.umd.edu` will give you a 1/3 chance of landing on the VM biggulp. If you logon to the VM, **perf will not work**. This is because the perf hardware counter events won't work on a virtual machine, you need access to the hardware itself.

So, you must ***specifically log on to krispykreme or cheezit***. Do this via the following
```bash
ssh <username>@krispykreme.cs.umd.edu
```
or
```bash
ssh <username>@cheezit.cs.umd.edu
```

## Building the Benchmark
Once you have logged into krispykreme or cheezit, clone this repository:
```bash
git clone git@github.com:ryansynk/cmsc818j_fall2023_Assignment2_GraphBIG.git
```
Then perform the following commands to build
```bash
cd cmsc818j_fall2023_Assignment2_GraphBIG
cd benchmark
make clean all
```

This will build all the various benchmarks. You can choose up to 5 that you'd like to collect data on. Some graph operations may be more familiar to you than others. In any case, to run one of the benchmarks, simply perform the following:
```bash
cd bench_BFS
perf stat ./bfs
```
You should then see a printout from perf. To run a different benchmark, replace `bench_BFS` and `./bfs` with the directory and executable of your choosing.

## Debugging

If you run `perf stat ./bfs` and see an output that looks like this
```bash
Performance counter stats for './bfs':

              1.21 msec task-clock:u                     #    0.663 CPUs utilized          
                 0      context-switches:u               #    0.000 /sec                   
                 0      cpu-migrations:u                 #    0.000 /sec                   
               104      page-faults:u                    #   86.277 K/sec                  
   <not supported>      cycles:u                                                    
   <not supported>      instructions:u                                              
   <not supported>      branches:u                                                  
   <not supported>      branch-misses:u                                             

       0.001818965 seconds time elapsed

       0.000000000 seconds user
       0.001644000 seconds sys

```
It's probably because you are on the VM. Does your terminal say `<username>@biggulp: `? This means you are on the VM. To fix, you must log out, and then log back in by using
```bash
ssh <username>@krispykreme.cs.umd.edu
```
or
```bash
ssh <username>@cheezit.cs.umd.edu
```

## Further information

Lifeng Nai, Yinglong Xia, Ilie G. Tanase, Hyesoon Kim, and Ching-Yung Lin. [GraphBIG: Understanding Graph Computing in the Context of Industrial Solutions](http://nailifeng.org/pubs/sc-graphbig.pdf), To appear in _the proccedings of the International Conference for High Performance Computing, Networking, Storage and Analysis(SC), Nov. 2015_


Documents can be found in the [GraphBIG-Doc](https://github.com/graphbig/GraphBIG-Doc) repository in the same graphbig organization. 

To cover the diverse features of graph data, GraphBIG present two types of graph data sets, real-world data and synthetic data. The real-world data sets can illustrate real graph data features, while the synthetic data can help workload characterizations because of its flexible data size.

The detailed dataset list and download links can be found at our [wiki page](https://github.com/graphbig/graphBIG/wiki/GraphBIG-Dataset "Dataset").

## Original Contributors
- Lifeng Nai, _Georgia Tech_ (lnai3 _at_ gatech.edu / lifeng _at_ us.ibm.com)  
- Yinglong Xia, _IBM Thomas J. Watson Research Center_ (yxia _at_ us _dot_ ibm _dot_ com)  
- Ilie G. Tanase, _IBM Thomas J. Watson Research Center_  
- Hyesoon Kim, _Georgia Tech_  
- Ching-Yung Lin, _IBM Thomas J. Watson Research Center_