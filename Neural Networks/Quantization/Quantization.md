# Quantization
## Introduction
Achieving efficient, real-time NNs with optimal accuracy requires rethinking the design, training, and deployment of NN models:
- Designing efficient NN model architectures
- Co-designing NN architecture and hardware together
- Pruning: neurons with small saliency (sensitivity) are removed (minimally affects the model output/loss function), resulting in a sparse computational graph. 
- Knowledge distillation: training a large model and then using it as a teacher to train a more compact model
- Quantization

## Basic Concepts of Quantization
### Problem Setup
Assume a NN has L layers with learnable parameters $W1, W2, ..., WL$ , with $θ$ denoting the combination of all such parameters. Optimize the function:

$$L(θ) = \frac{1}{N}\sum_{i=1}^N l(xi, yi; θ)$$

- $x_i,y_i$ : input data and label
- $l()$ : loss function
- $N$ : total data points

Denote:
-   $h_i$ : input hidden activations of the ith layer 
- $a_i$ : corresponding output hidden activation

Assume that $\theta$ is stored in floating point precision

Quantization goal:

Reduce the precision of both the **parameters (θ)**, as well as the **intermediate activation maps** (i.e., hi, ai) to low-precision, with minimal impact on the **generalization power/accuracy of the model**.

### Uniform Quantization
Define a function that can quantize NN weights and activations to a finite set of values.


$$Q(r) = Int(r/S) − Z$$

- $r$ : real valued input (activation or weight)
- $S$ : real valued scaling factor
- $Z$ : an integer zero point
- $Int$ : maps a real value to an integer value

Dequantization: $\hat{r} = S(Q(r) + Z).$

### Symmetric and Asymmetric Quantization

Choice of the scaling factor $S$

$S = \frac{β−α }{2^b − 1}$

- $[α, β]$ : the clipping range.
- $b$ : quantization bit width.

Two types of quantization:
- Symmetric: $α = −β.$ , $−α = β = max(|r_{max}|, |r_{min}|).$ 
  
  Symmetric quantization is widely adopted because zeroing out the **zero point can lead to reduction in computational cost during inference**
- Asymmetric: i.e., $α = r_{min},  β = r_{max}$.

Using min/max approach is susceptible to outlier data in the activations.

Approaches to address this:
- Use **percentile**: the $i$-th largest/smallest values are used as $β/α$.
- Select $α$ and $β$ to minimize KL divergence (i.e., information loss) between the real values and the quantized values .

### Range Calibration Algorithms: Static vs Dynamic Quantization

Another important differentiator of quantization methods is **when the clipping range is determined**：
- **Dynamic quantization**: range is dynamically calculated for each activation map during runtime.
- **Static quantization**: clipping range is pre-calculated and static during inference.

### Quantization Granularity

- Layerwise Quantization: 
- Groupwise Quantization:
- Channelwise Quantization:
- Sub-channelwise quantization: 

### Non-Uniform Quantization

**Quantization steps** as well as **quantization levels** are allowed to be non-uniformly spaced: 

$$Q(r) = X_i, if \space r ∈ [∆_i, ∆_{i+1})$$

- $X_i$ : discrete quantization levels 
- $∆_i$ : quantization steps

Some examples:

- Use a logarithmic distribution
- Binarycode-based quantization: a real-number vector $r ∈ R^n$ is quantized into $m$ binary vectors by representing $r ≈ ∑_{i=1}^m α_ib_i$ , with the scaling factors $α_i ∈ R$ and the binary vectors $b_i ∈ \{−1, +1\}^n$ .

To further improve, some formulate non-uniform quantization as an optimization problem:

$$\mathop{min}\limits_Q ‖Q(r) − r‖^2$$

So the quantizer itself can also be jointly trained with the model parameters.(learnable quantizers).

**Restrictions**: Non-uniform quantization schemes are typically difficult to deploy efficiently on general computation hardware, e.g., GPU and CPU.

### Fine-tuning Methods

It is often necessary to adjust the parameters in the NN after quantization. It can be performed by:
- Retraining the model: QuantizationAware Training (QAT)
  
  Quantization may introduce a perturbation to the trained model parameters, and this can push the model away from the point to which it had converged when it was trained with floating point precision. 
  
  It is possible to address this by re-training the NN model with quantized parameters so that the model can converge to a point with better loss.

  QAT: the usual forward and backward pass are performed on the quantized model in floating point, but the model parameters are quantized after each gradient update
- Without re-training: Post-Training Quantization (PTQ).

![alt text](../../assets/MarkdownImg/image-11.png)


### Stochastic Quantization