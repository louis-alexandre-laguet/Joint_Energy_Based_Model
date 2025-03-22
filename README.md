# Joint Energy-Based Model

JEM (*Joint Energy-Based Model*) is an energy-based model (EBM) that combines **classification** and **image generation**. It simultaneously learns the probability of an image $p_{\theta}(x)$ and the conditional probability of a class $p_{\theta}(y | x)$, enabling it to classify images while also generating new data.

JEM is based on a **convolutional neural network** that extracts features from images and produces two main outputs:

- **Energy**: $E_{\theta}(x)$ measures the plausibility of the image in the space learned by the model.
- **Classification logits**: $f_{\theta}(x)$ are used to predict the class of the image.

The training of JEM relies on several objectives:
1. **Supervised classification**: A standard classification loss, such as cross-entropy, is used to associate an image with a label.
2. **Contrastive divergence**: A regularization term that helps distinguish true images from generated samples.
3. **Energy regularization**: A constraint on $E_{\theta}(x)$ to improve the model’s stability and robustness.

JEM generates images using a **Langevin dynamics** approach:
1. **Initialization**: The process starts with an image consisting of random noise.
2. **Progressive refinement**: An **MCMC (Monte Carlo Markov Chain)** algorithm gradually modifies the image to make it more realistic. At each iteration, the image is adjusted by reducing its energy, moving it closer to a plausible sample from the model.
3. **Diversification**: A **resampling buffer** is used to avoid generating the same images repeatedly and ensure a greater variety in the produced samples.

With this approach, JEM unifies **classification** and **generation**, fully exploiting the properties of energy-based models.
