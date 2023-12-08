# mpas-report

## Load module

Module load pio/openmpi/intel/2.6.2

## get source code

https://github.com/MPAS-Dev/MPAS-Model.git

cd MPAS-Model

### Build

using [build-script](build-mpas.bash)

In the script we set CORE=atmosphere OPENMP=false and a few environment settings. We can also set PERSICION=SINGLE

bash ../build-mpas.bush make ifort.

We should have the executable `atmosphere_model`

## Download benchmark

wget https://www2.mmm.ucar.edu/projects/mpas/benchmark/v7.0/MPAS-A_benchmark_60km_v7.0.tar.gz

cd /scratch/work/scc23/mpas-a-benchmark
tar -vxzf SRC/MPAS-A_benchmark_60km_v7.0.tar.gz

cd /scratch/work/scc23/mpas-a-benchmark/MPAS-A_benchmark_60km_v7.0

rm -rf  *.DBL *.TBL RRTMG_*

link files from source code folder

ln -s $PATH_TO_SOURCE_CODE_FOLDER/MPAS-Model/atmosphere_model .

ln -s $PATH_TO_SOURCE_CODE_FOLDER/MPAS-Model/src/core_atmosphere/physics/physics_wrf/files/* .

### Meshes

cd ..

wget https://mpas-dev.github.io/atmosphere/atmosphere_meshes.html

cd MPAS-A_benchmark_60km_v7.0

cp ../meshes/x1.163842.gr* .

## Execute

srun --nodes=1 --tasks-per-node=48 --mem=180GB --time=12:00:00 ./atmosphere_model