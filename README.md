# Bibliotheca-Alexandria-Tensorflow
Submit a job to import tensorflow in Bibliotheca Alexandria's cluster

## Tensorflow installation guide

There is no root access on the cluster, so we can only install python packages with pip/ anaconda package managers AND also to specify that the installation directory is in the ‘HOME/data’ directory not the HOME directory.
I tried PIP but I was stuck with some problems. Thankfully, anaconda succeeded. So, let's get started.

### Load some modules:
To load the Python module:
```
module load Python/2.7.3-intel-2016b
```

There was a dependency that requires libjpeg to be installed (I forgot what was the error then), so I loaded this module:
```
module load libjpeg-turbo/1.5.0-intel-2016b
```

To load the cuDNN/ CUDA libraries (these are required for the GPU implementation):
```
module load cuDNN/5.1-CUDA-8.0.44
```

And the module that manages the installation of python packages:
```
module load Anaconda2/4.0.0
```

### Configure Anaconda to install packages in another directory than the HOME directory due to size limit:
Create a new conda environment:
```
conda create -p ~/data/conda_packages -m
```

Activate the environment, change USER_NAME with your username literal:
```
source activate /home/USER_NAME/data/conda_packages
```

Change download directory of source packages to be in the data folder also
```
nano ~/.condarc
mkdir ~/data/conda_packages_cache
```

Then add the following two lines in the ~/.condarc file, change USER_NAME with your username literal:
```
envs_dirs:
  - /home/USER_NAME/data/conda_packages_cache/
```

Let the changes take effect:
```
source ~/.condarc
```

Install tensoflow-gpu
```
conda install -c anaconda tensorflow-gpu
```

### Submit a job to the cluster:
Go to data directory, and then:

```
git clone https://github.com/Mohamed-Kassem/Bibliotheca-Alexandria-Tensorflow
cd Bibliotheca-Alexandria-Tensorflow
sbatch tensorflow_job.sh
```
