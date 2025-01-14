# Framework for FDPP (Fatigue Damage Prognostics Problem)

FDPP is an open-source framework for generating large synthetic data sets specific to fatigue damage prognosticx problems, in particular for an aerospace structure problem (e.g. fuselage panels). 

This work was carried out within the PREDICT project, involving Anass Akrim, Christian Gogu (Principal Investigator), Thomas Guillebot de Nerville, Michel Salaun, Paul Strahle, Rob Vingerhoeds and Brondon Waffa Pagou at the University of Toulouse (Institut Clément Ader and ISAE-SUPAERO DISC). If you find this repository helpful, please cite our work:

```
@INPROCEEDINGS{ICPHM,
  author={Akrim, Anass and Gogu, Christian and Guillebot de Nerville, Thomas  and Strähle, Paul and Waffa Pagou, Brondon and Salaün, Michel and Vingerhoeds, Rob},
  booktitle={2022 IEEE International Conference on Prognostics and Health Management (ICPHM)}, 
  title={A Framework for Generating Large Data Sets for Fatigue Damage Prognostic Problems}, 
  year={2022},
  pages={25-33},
  doi={10.1109/ICPHM53196.2022.9815692}}
```


# Description

The idea behind this project is to propose a framework and software code for synthetically generating large training data sets for a realistic fatigue damage prognostics problem. 

The project is illustrated with a realistic case study on the Jupyter Notebook ``Illustration_CaseStudy.ipynb``, i.e. a RUL estimation problem where the available input data is strain gauge data, and the applicability of some of the most commonly used DL models to address failure prognostics has been studied (RNN, LSTM, GRU, 1D-CNN and TCN), available on the ``models`` directory. Keras Tensorflow library was used, with Tensorflow version 2.3.0, and CUDA 11.0. Models were trained mainly on NVIDIA V100 GPUs.


# Generating set

This code was tested on Python 3.7, Pandas 0.25.1, Ubuntu 18.04, and Anaconda 4.7.11. This repository can be installed using the following command :

```
git clone https://github.com/ansak95/FrameworkFDPP.git
cd FrameworkFDPP

conda create -n env_fdpp python=3.7 pandas=0.25.1
conda activate env_fdpp
pip install -r requirements.txt
```

You can generate the illustration dataset (training/validation/testing) by using the `python main.py` command as follows :

```
python main.py 
```
Or using a shell script that executes the configuration actions, allowing to modify the parameters directly on the script : 

```
bash generate.sh 
```


In order to generate a dataset with different parameters, use the `python main.py` command and set optional arguments if needed, such that :

```
python main.py               --folder_data            data \
                             --E                      71.7e9 \
                             --nu                     0.33 \
                             --sigma_inf              78.6e6 \
                             --K_IC                   19.7 \
                             --nb_gauges              3 \
                             --x_gauge                0.003 0.014 0.025 \
                             --y_gauge                0.014 0.014 0.014  \
                             --theta_gauges           45 \
                             --a_0_mean               0.001 \
                             --m_mean                 3.5 \
                             --m_std                  0.125 \
                             --C_mean                 1e-10 \
                             --n_train                1000  \
                             --n_val                  100 \
                             --n_test                 100 \
                             --delta_k                500 \
                             --lb_star                0.33 \
                             --ub_star                0.95 
 
```


Arguments dictionary and the the dataframes which are generated are saved to `data` folder by default.
The detail of command-line usage is as follows:

```

python main.py -h
usage: main.py [-h] [--folder_data FOLDER_DATA] [--E E] [--nu NU] [--sigma_inf SIGMA_INF] [--K_IC K_IC] [--nb_gauges NB_GAUGES] [--x_gauge X_GAUGE]
                          [--y_gauge Y_GAUGE] [--theta_gauges THETA_GAUGES] [--a_0_mean A_0_MEAN] [--m_mean M_MEAN] [--m_std M_STD] [--C_mean C_MEAN] [--n_train N_TRAIN]
                          [--n_val N_VAL] [--n_test N_TEST] [--delta_k DELTA_K] [--lb_star LB_STAR] [--ub_star UB_STAR]

Generate_Set

optional arguments:
  -h, --help            show this help message and exit
  --folder_data FOLDER_DATA
                        Set the folder path
  --E E                 Young's modulus of the structure
  --nu NU               Poisson's ratio of the structure
  --sigma_inf SIGMA_INF
                        Maximum stress intensity
  --K_IC K_IC           Fracture toughness of the structure
  --nb_gauges NB_GAUGES
                        Number of gauges
  --x_gauge X_GAUGE     x position of the gauges placed
  --y_gauge Y_GAUGE     y position of the gauges placed
  --theta_gauges THETA_GAUGES
                        Angle of the gauges placed
  --a_0_mean A_0_MEAN   Initial half crack length mean in [m]
  --m_mean M_MEAN       m mean 
  --m_std M_STD         m std 
  --C_mean C_MEAN       C mean 
  --n_train N_TRAIN     Number of training structures
  --n_val N_VAL         Number of validation structures
  --n_test N_TEST       Number of testing structures
  --delta_k DELTA_K     Data collection interval
  --lb_star LB_STAR     lower boundary (used for generating t* for the test set)
  --ub_star UB_STAR     upper boundary (used for generating t* for the test set)
```



# Acknowledgements

◦ This work was partially funded by Occitanie region under the Predict project. This funding is gratefully acknowledged. 

◦ This work has been carried out on the supercomputers PANDO (ISAE Supaero, Toulouse) and Olympe (CALMIP, Toulouse, project n°21042). Authors are grateful to ISAE Supaero and CALMIP for the hours allocated to this project.

◦ The authors would like to thank Christian Thomas Nitschke for his initial input on modelling the crack growth problem.
