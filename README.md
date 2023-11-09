# Project-Giannis---Senior-Design
---

### Basketball Free Throw Prediction using Skeletal Movement

#### Project Overview:
The primary objective was to predict and determine whether a person is going to make a free throw based on their skeletal movement. 

**My role was the main machine learning engineer in my group that proposed and led the data acquisition phase and the model designing phase.** 

#### Data Collection:
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

#### Methodology:

1. **Data Preprocessing**: [code](https://github.com/tyrellto/Giannis-Free-Throw-Prediction/blob/main/sorting.ipynb)
   - Each sample taken from individuals was transformed from time series skeletal movement data into a flattened vector representing all joints (including elbow, shoulder, neck, wrist, knees, ankles, hip, etc.).
   
2. **Feature Selection**:
   - Mutual information was employed to discern which joints contributed most significantly to the model's performance. This choice was made despite the challenges posed by non-stationary, non-linear data. In hindsight, other metrics or techniques like auto-encoders to map the numerous features onto a latent space or UMAP for visualization could have been explored.
   ![image](https://github.com/dominusoctane/Project-Giannis---Senior-Design/assets/61175343/b5fa3ea5-6c07-4828-8afb-0de8fc309da6)

3. **Modeling**: [code](https://github.com/tyrellto/Giannis-Free-Throw-Prediction/blob/main/FreeThrowTabularPredict.ipynb)
   - CatBoost was chosen as the primary model to predict the outcome of the free throws. On average, an accuracy of 67% was achieved across all team members. 
   - Future considerations: Given the time series nature of the data, models like LSTMs, GRUs, or transformer-based architectures could be explored further to learn from the long-term and short-term temporal/spatial relationships between the joints across different time stamps.

#### Results:
An average accuracy of 67% was achieved in predicting free throw outcomes based on skeletal movements.

#### Visualizations:
[Note: The notebooks contain visualizations detailing the analysis and outcomes. Please check the specific sections for graphical representations.]

#### Technologies Used:
- Python
- Brekel Body Software
- Depth Perception Camera

### Key Takeaways / Future Work: 
- If I had more time 

---
