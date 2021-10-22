# LyaNet: A Lyapunov Framework for Training Neural ODEs

Provide the model type```--config-name``` to train and test models 
configured as those shown in the paper. 

## Classification Training
For the code assumes the project root is the current directory.

Example commands:

```bash
python sl_pipeline.py --config-name classical +dataset=MNIST
```

Tensorboards are saved to ```run_data/tensorboards``` and can be viewed by 
running:

```bash
tensorboard --logdir ./run_data/tensorboards --reload_multifile True
```

## Adversarial Robustness

Assuming the current directory is ``robustness``. Notice that the model file 
name will be different depending on the dataset and modeel combination you 
have run. This path provided should provide an idea of the path structure 
where models are stored.

These scripts will print the testing error, followed by the testing error 
with adversarial robustness. Notice adversarial testing requires 
significantly more resources.

### L2 Adversarial robustness experiments

```bash
python untargerted_robustness.py --config-name classical +dataset=MNIST
+model_file='../run_data/tensorboards/d.MNIST_m.ClassicalModule(RESNET18)_b.128_lr.0.01_wd.0.0001_mepoch120._sd0/default/version_0/checkpoints/epoch=7-step=3375.ckpt'
+norm="2"
```

### L Infinity Adversarial robustness experiments

```bash
python untargerted_robustness.py --config-name classical +dataset=MNIST
+model_file='../run_data/tensorboards/d.MNIST_m.ClassicalModule(RESNET18)_b.128_lr.0.01_wd.0.0001_mepoch120._sd0/default/version_0/checkpoints/epoch=7-step=3375.ckpt'
+norm="2"
```

### Datasets supported

* ```MNIST```
* ```FashionMNIST```
* ```CIFAR10```
* ```CIFAR100```

### Models Supported

* ```anode``` : Data-controlled dynamics with ResNet18 Component trained 
  through solution differentiation
* ```classical```: ResNet18
* ```lyapunov```: Data-controlled dynamics with ResNet18 Component trained 
  with LyaNet
* ```continuous_net```: ContinuousNet from [1] trained through solution 
  differentiation
* ```continuous_net_lyapunov```: ContinuousNet from [1] trained with LyaNet 

##A Note on Libs

Both Nero[2] and ContinuousNet[1] are modified to work with LyaNet. Forks are 
included here without history for the purposes of anonymity.

##References
1. [Continuous-in-Depth Neural Networks](https://arxiv.org/abs/2008.02389) 
   [Code](https://github.com/afqueiruga/ContinuousNet)
2. [Learning by Turning: Neural Architecture Aware Optimisation](https://arxiv.org/abs/2102.07227)
[Code](https://github.com/jxbz/nero)