# Tutorial on NNP MD simulation for methane

[![DOI:10.1016/B978-0-323-90049-2.00001-9](https://img.shields.io/badge/DOI-10.1016%2FB978--0--323--90049--2.00001--9-blue)](https://doi.org/10.1016/B978-0-323-90049-2.00001-9)

This is a tutorial for the following chapter. Please cite the chapter if you follow this tutorial:

Jinzhe Zeng, Liqun Cao, Tong Zhu (2023). Chapter 12 - Neural network potentials. Pavlo O. Dral (Eds.), _Quantum Chemistry in the Age of Machine Learning_ (pp. 279-294), Elsevier.

## Preparation

Before starting this tutorial, you need to download and install the following software:

- [DeePMD-kit](https://github.com/deepmodeling/deepmd-kit/) with [LAMMPS](https://github.com/lammps/lammps) support
- [ReacNetGenerator](https://github.com/tongzhugroup/reacnetgenerator)

It's also recommended to have a GPU environment.

Download this repository:

```sh
git clone https://github.com/tongzhugroup/Chapter13-tutorial
cd Chapter13-tutorial
```

## Training the model

Execute

```sh
dp train methane_param.json
```

After the training is completed, freeze and compress the model:

```sh
dp freeze -o graph.pb
```

You will get the model file called `graph.pb`. We've provided `graph.pb` in this repository to continue the next step.

Then compress the model:
```sh
dp compress -i graph.pb -o graph_compressed.pb -t methane_param.json
```

## Running the simulation

Execute

```sh
lmp -in input.lammps
```

## Analyze the simulation

Execute

```sh
reacnetgenerator -i methane.lammpstrj --dump -a C H O --nohmm
```

