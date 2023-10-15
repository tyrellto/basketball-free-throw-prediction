# Project-Giannis---Senior-Design
---

### Free Throw Prediction using Skeletal Movement

#### Project Overview:
This project was undertaken as a part of the senior design initiative. The primary objective was to predict and determine whether a person is going to make a free throw based on their skeletal movement. 

#### Data Collection:
Data was captured using live motion capture of team members attempting to do free throws from a designated distance. The software employed for this task was **Brekel Body v3** in conjunction with three depth perception cameras.

#### Methodology:

1. **Data Preprocessing**: 
   - Each sample taken from individuals was transformed from time series skeletal movement data into a flattened vector representing all joints (including elbow, shoulder, neck, wrist, knees, ankles, hip, etc.).
   
2. **Feature Selection**:
   - Mutual information was employed to discern which joints contributed most significantly to the model's performance. This choice was made despite the challenges posed by non-stationary, non-linear data. In hindsight, other metrics or techniques like auto-encoders to map the numerous features onto a latent space or UMAP for visualization could have been explored.
   ![image](https://github.com/dominusoctane/Project-Giannis---Senior-Design/assets/61175343/b5fa3ea5-6c07-4828-8afb-0de8fc309da6)

3. **Modeling**:
   - CatBoost was chosen as the primary model to predict the outcome of the free throws. On average, an accuracy of 67% was achieved across all team members. 
   - Future considerations: Given the time series nature of the data, models like LSTMs, GRUs, or transformer-based architectures could be explored further to learn from the long-spatial and short-spatial relationships between the joints across different time stamps.

#### Results:
An average accuracy of 67% was achieved in predicting free throw outcomes based on skeletal movements.

#### Visualizations:
[Note: The notebook contains visualizations detailing the analysis and outcomes. Please check the specific sections for graphical representations.]

#### Technologies Used:
- Python
- Brekel Body Software
- Depth Perception Camera

---
