
## 1. Objective
The objective of this assignment is to learn an **unknown probability density function (PDF)** of a transformed random variable using **only sample data**, without assuming any parametric form of the distribution.  
A **Generative Adversarial Network (GAN)** is used to implicitly model the probability distribution of the transformed variable.

## 2. Dataset Description
- Dataset used: **India Air Quality Dataset**
- Feature selected: **NO₂ (Nitrogen Dioxide) concentration**
- The dataset consists of real-valued air pollution measurements.
- Missing values are removed before processing.
- Only the NO₂ column is used as input, as specified in the assignment.

## 3. Data Transformation
Each NO₂ concentration value \( x \) is transformed using the nonlinear transformation:

\[
z = x + a_r \sin(b_r x)
\]

### Transformation Parameters
- University Roll Number \( r = 102303778 \)
- \( a_r = 0.5 \times (r \bmod 7) = 1.5 \)
- \( b_r = 0.3 \times ((r \bmod 5) + 1) = 1.5 \)

After transformation, the variable \( z \) is **standardized** to ensure stable GAN training.

## 4. Methodology

### 4.1 GAN Overview
A Generative Adversarial Network consists of two neural networks:
- **Generator (G)**: Generates fake samples resembling real data
- **Discriminator (D)**: Distinguishes between real and fake samples

Both networks are trained simultaneously in an adversarial manner.

### 4.2 Generator Architecture
- Input: Noise sampled from standard normal distribution \( \mathcal{N}(0,1) \)
- Layers:
  - Dense (32) + LeakyReLU
  - Dense (32) + LeakyReLU
  - Dense (1)
- Output: Generated samples \( z_f \)

### 4.3 Discriminator Architecture
- Input: Real or generated \( z \) values
- Layers:
  - Dense (16) + LeakyReLU
  - Dense (16) + LeakyReLU
  - Dense (1) with Sigmoid activation
- Output: Probability of input being real

### 4.4 Training Details

| Parameter | Value |
|---------|------|
| Optimizer | Adam |
| Learning Rate | 0.0002 |
| Batch Size | 64 |
| Epochs | 3000 |
| Loss Function | Binary Cross Entropy |

The discriminator is trained to correctly classify real and fake samples, while the generator is trained to fool the discriminator.

## 5. Result Generation

After training the GAN:
1. A large number of samples are generated using the trained generator.
2. The probability density function is estimated using:
   - **Histogram Density Estimation**
   - **Kernel Density Estimation (KDE)**

## 6. Results

### 6.1 Result Table

| Method | Description |
|------|------------|
| Histogram | Shows approximate distribution of generated samples |
| KDE | Provides smooth estimation of learned PDF |
| GAN Samples | Closely resemble real transformed data |

### 6.2 Result Graphs

#### (a) Histogram of GAN Generated Samples
- Displays the frequency distribution of generated \( z \) values.
- Confirms that the generator produces realistic samples.

#### (b) KDE Plot of Generated Samples
- Shows a smooth probability density curve.
- Captures major modes of the distribution.

#### (c) Comparison of Real vs GAN PDF
- KDE of real transformed data vs KDE of GAN-generated data.
- Both curves show strong overlap, indicating successful learning.

## 7. Observations
- The GAN effectively learns the underlying distribution without assuming any parametric form.
- Mode coverage is satisfactory with minimal mode collapse.
- Training initially shows instability but stabilizes after sufficient epochs.
- KDE provides better visualization compared to histogram-based estimation.

## 8. Conclusion
This assignment demonstrates that a GAN can successfully learn an unknown probability density function using only data samples.  
The generated samples closely match the real data distribution, validating the effectiveness of GANs for non-parametric density estimation.


---
