# Quantization
## Introduction
Achieving efficient, real-time NNs with optimal accuracy requires rethinking the design, training, and deployment of NN models:
- Designing efficient NN model architectures
- Co-designing NN architecture and hardware together
- Pruning: neurons with small saliency (sensitivity) are removed (minimally affects the model output/loss function), resulting in a sparse computational graph. 
- Knowledge distillation: training a large model and then using it as a teacher to train a more compact model
- Quantization

## General History of Quantization
