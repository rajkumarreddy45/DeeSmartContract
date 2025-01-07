# DeeSmartContract


This repo is a python implementation of smart contract vulnerability detection using graph neural networks (DR-GCN).


## Requirements
### Required Packages
* **python** 3+ (python 3.7 used in our project)
* **PyTorch** 1.0.0
* **numpy** 1.18.2
* **sklearn** 0.20.2

Run the following script to install the required packages.
```
pip install --upgrade pip
pip install torch==1.0.0
pip install numpy==1.18.2
pip install scikit-learn==0.20.2
```


## Citation
Please use this citation in your paper if you refer to our [paper](https://www.ijcai.org/Proceedings/2020/0454.pdf) or code.
```
@inproceedings{zhuang2020smart,
  title={Smart Contract Vulnerability Detection using Graph Neural Network.},
  author={Zhuang, Yuan and Liu, Zhenguang and Qian, Peng and Liu, Qi and Wang, Xiang and He, Qinming},
  booktitle={IJCAI},
  pages={3283--3290},
  year={2020}
}
``` 


## Running project
* To run program, please use this command: python3 SMVulDetector.py.
* In addition, you can set specific hyper-parameters, and all the hyper-parameters can be found in `parser.py`.

Examples:
```shell
python3 SMVulDetector.py --dataset training_data/REENTRANCY_CORENODES_1671
python3 SMVulDetector.py --dataset training_data/REENTRANCY_CORENODES_1671 --model gcn_modify --n_hidden 192 --lr 0.001 -f 64,64,64 --dropout 0.1 --vector_dim 100 --epochs 50 --lr_decay_steps 10,20 
```

Using script：
Repeating 10 times for different seeds with `train.sh`.
```shell
for i in $(seq 1 10);
do seed=$(( ( RANDOM % 10000 )  + 1 ));
python3 SMVulDetector.py --model gcn_modify --seed $seed | tee logs/smartcheck_"$i".log;
done
```
Then, you can find the training results in the `logs/`.


### Dataset
For original dataset, please turn to the dataset [repo](https://github.com/Messi-Q/Smart-Contract-Dataset).

The normalized train data can be found in
`training_data/REENTRANCY_CORENODES_1671`, `REENTRANCY_FULLNODES_1671`

Note that the instruction of constructing the dataset can be found in the [GraphLearning](https://ls11-www.cs.tu-dortmund.de/staff/morris/graphkerneldatasets), and the `XXX_node_attributes` can be obtained using our designed [tools](https://github.com/Messi-Q/SourceGraphExtractor). 


### Reference
1. A fraction of the code reuses the code of [graph_unet](https://github.com/bknyaz/graph_nn).
2. Thomas N. Kipf, Max Welling, Semi-Supervised Classification with Graph Convolutional Networks, ICLR 2017.
