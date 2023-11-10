# Project-Giannis---Senior-Design
---
**Table of Contents**
- [Project Overview](#project-overview)
- [Data Collection](#data-collection)
- [Methodology](#methodology)
  - [Data Preprocessing](#data-preprocessing)
  - [Feature Selection](#feature-selection)
  - [Modeling](#modeling)
- [Key Takeaways / Future Work](#key-takeaways--future-work)


## Basketball Free Throw Prediction using Skeletal Movement

### Project Overview:
The primary objective was to predict and determine whether a person is going to make a free throw based on their skeletal movement. 

**My role was the main machine learning engineer in my group that proposed and led the data acquisition phase and the model designing phase.** 

<p align="center">
  <img src="https://github.com/tyrellto/Giannis-Free-Throw-Prediction/assets/61175343/9e6c03d2-3c26-4ad8-8c60-9c6d0e012687" width="400" alt="MJ Freethrow"/>
</p>

### Data Collection:
Data was captured using live motion capture of team members attempting to do basketball free throws from a designated distance. The software employed for this task was **Brekel Body v3** [link](https://brekel.com/brekel-body-v3/) in conjunction with three depth perception Azure cameras. Brekel Body v3 contains pretrained body tracking models to use for inference with a NVIDIA GPU(A high end one like a RTX 2080 is recommended). We used one of our teammates computers to do inference, where we had the three cameras were connected to his PC.

Below is the type of camera that we used: [link to buy](https://www.microsoft.com/en-us/d/azure-kinect-dk/8pp5vxmd9nhq?activetab=pivot:overviewtab)

<p align="center">
  <img src="https://github.com/tyrellto/Giannis-Free-Throw-Prediction/assets/61175343/0500f90c-7360-4b12-bc76-3217dc4fc832" width="400" alt="Azure Kinect KS"/>
</p>

Here is an example of how the data is collected with the following video as reference (not me in video):

<p align="center">
  <a href="http://www.youtube.com/watch?v=NBZdTpLwhLA" title="Motion Capture">
    <img src="http://img.youtube.com/vi/NBZdTpLwhLA/0.jpg" width="400" alt="Motion Capture"/>
  </a>
</p>

We would position the cameras in a specific orientation like in the following diagram with the middle camera in the back, and side cameras 25-45 degrees angled from the center (not to scale):

<p align="center">
  <img width="400" alt="Screenshot 2023-11-09 at 2 58 41 PM" src="https://github.com/tyrellto/Giannis-Free-Throw-Prediction/assets/61175343/dbc7bf0a-bab1-4543-892d-2129e8f65f80">
</p>

### Methodology:

1. **Data Preprocessing**: [code](https://github.com/tyrellto/Giannis-Free-Throw-Prediction/blob/main/sorting.ipynb)
   - Each sample taken from individuals was transformed from time series skeletal movement data into a flattened vector representing all joints (including elbow, shoulder, neck, wrist, knees, ankles, hip, etc.).
   - The figure below shows the high level process, where each recording for a person for all joints' time series data flattened to one singular feature vector:
  <p align="center">
    <img width="1000" alt="Screenshot 2023-11-09 at 3 43 13 PM" src="https://github.com/tyrellto/Giannis-Free-Throw-Prediction/assets/61175343/be9108c0-cd62-481d-865d-115a90bff827">
  </p>

2. **Feature Selection**:
   - Mutual information was employed to discern which joints contributed most significantly to the model's performance. This choice was made despite the challenges posed by non-stationary, non-linear data. In hindsight, other metrics or techniques like auto-encoders to map the numerous features onto a latent space or UMAP for visualization could have been explored.
   ![image](https://github.com/dominusoctane/Project-Giannis---Senior-Design/assets/61175343/b5fa3ea5-6c07-4828-8afb-0de8fc309da6)

3. **Modeling**: [code](https://github.com/tyrellto/Giannis-Free-Throw-Prediction/blob/main/freethrow_tabular_predict.ipynb)
   - CatBoost was chosen as the primary model to predict the outcome of the free throws. On average, an accuracy of 67% was achieved across all team members. 
   - Future considerations: Given the time series nature of the data, models like LSTMs, GRUs, or transformer-based architectures could be explored further to learn from the long-term and short-term temporal/spatial relationships between the joints across different time stamps.

### Key Takeaways / Future Work: 

When applying machine learning models to determine if a person can make a free throw based on skeletal movement data, I faced several challenges. Here's a detailed breakdown of each problem and the approaches I could take to address them:

1. **Low Quality of Samples**:
   - **Problem:**: The quality of skeletal movement data is crucial. Low-quality data can be due to poor resolution, inaccuracies in skeletal tracking, or irrelevant features being captured.
   - **Approach:**: I can enhance data quality by preprocessing the data with filters and normalization techniques. Implementing techniques like Principal Component Analysis (PCA) can help in focusing on the most relevant features. Furthermore, I might use advanced data augmentation methods to artificially enhance the dataset, like simulating variations in the free throw techniques.

2. **Low Number of Samples**:
   - **Problem:**: Machine learning models require a substantial amount of data to learn effectively. A low number of samples can lead to overfitting, where the model learns the training data too well and performs poorly on unseen data.
   - **Approach:**: To combat this, I can utilize data augmentation techniques to increase the dataset size artificially, such as by slightly altering the existing samples or using generative models to create new samples. Another avenue is to implement transfer learning where a model trained on a large dataset in a similar domain is adapted to my specific task.

3. **High Noise to Signal Ratio**:
   - **Problem:**: A high amount of noise in the data can obscure the underlying patterns that correlate with successful free throws, making it challenging for the model to learn effectively. **Notably, each person's free throw form is unique.**
   - **Approach:**: To improve the signal-to-noise ratio, I could apply noise reduction techniques such as smoothing filters or denoising autoencoders. Additionally, collecting more targeted data where the noise factors are controlled or minimized during the data collection phase could also be beneficial.

4. **Needs More Sophisticated Methods for Determining Free Throw Off Skeletal Data**:
   - **Problem:**: Basic machine learning models might not capture the complexity of the movements that predict a successful free throw.
   - **Approach:**: I should explore more sophisticated models like deep learning, specifically Recurrent Neural Networks (RNNs) or Long Short-Term Memory networks (LSTMs) that can better capture temporal dependencies in movement data. These models are more suited to sequence prediction problems like analyzing time-series skeletal movement data.

5. **Need Better Hardware**:
   - **Problem:**: Accurate skeletal movement capture often requires high-end hardware, which can be cost-prohibitive.
   - **Approach:**: I could seek partnerships or grants to access better hardware. Alternatively, I can research and develop algorithms that are more robust to lower-quality data, perhaps by focusing on core movement patterns that are less dependent on high-resolution data.

6. **Needs Better Motion Capture Techniques**:
   - **Problem:** The precision of motion capture techniques can significantly impact the quality of skeletal data. Inferior motion capture can introduce errors and inaccuracies.
   - **Approach:** I can explore newer motion capture technologies that provide higher precision without dramatically increasing costs. Using multiple sensors or cameras can also help improve the data quality. Additionally, incorporating calibration routines and error-correction algorithms in the data processing pipeline can mitigate the effects of inaccurate motion capture.

**TL;DR: To tackle the challenges of applying machine learning to free throw predictions from skeletal movement data:**

1. **Improve Sample Quality**: Use data preprocessing to filter out noise and focus on relevant features; consider data augmentation to enhance the dataset.
2. **Increase Sample Size**: Employ data augmentation and transfer learning to bolster the training set and prevent overfitting.
3. **Reduce Noise**: Implement noise reduction techniques and collect higher quality data with less background noise.
4. **Employ Advanced Models**: Utilize sophisticated neural networks like RNNs or LSTMs to capture the complex temporal patterns in skeletal data.
5. **Access Better Hardware**: Seek funding for high-quality motion capture hardware or develop algorithms that perform well with lower-quality data.
6. **Enhance Motion Capture Techniques**: Invest in advanced motion capture technology and improve data accuracy with calibration and error-correction algorithms.


---
