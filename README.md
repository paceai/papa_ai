# Walking with PACE — Personalized and Automated Coaching Engine
TF code for Boost and sense action prediction for PACE paper  
The code repository has two IPython Notebooks. 
* Boost selection model 
* Sense selection model 

We automate the coach action in the human coaching group using machine learning. Coaches in the direct group personalized the coaching conversation based on participant characteristics and needs. The user information, coach actions and user responses were collected in detail during the study. The conversations were further cleaned and annotated by the annotators to facilitate the ML models to train and imitate the coach actions conditioned on participants. The annotation protocol and semantics of each data point is explained in supplementary material. Each data point corresponds to a block of conversation where the coach is using a combination of motivation, ability or propensity enhancement strategies to nudge participants to improve step count and consistency. Each data point is defined by a triplet of user characteristics, perceived and sensed state of motivation, propensity and ability and coach actions. Two ML models are trained in stages to predict two kinds of coach actions (Table \ref{table:ml-all}A). First ML model is trained to predict if the coach used sense (sub classify as motivation, ability, and propensity) or boost actions based on user personas and conversation stage. The second ML model predicts the specific boost (motivation, ability, and propensity) action taken by the coach based on the user state and goals. The models are broken into stages to make them modular. The first model which predicts the sense action can also be replaced by simpler heuristics based on user step count history. Since the second model can predict personalized nudge for users, we focus more on the “Boost selection model” going forward. Sense prediction model is similar and only the differences are highlighted wherever necessary. 

Three multi label ML variants are used to train the “nudge prediction model”. Each model has three binary classification loss functions to predict if the coach used motivation, ability and propensity as a nudge independently. A single conversation based nudge may subsume motivation, ability and propensity translating as labels for the data-point. They may also deploy a different strategy which translates to data-point with no labels for each of the above three strategies. Logistic regression, Deep and wide neural network and XGboost trees are built on the Tensor Flow 2.8 platform using Keras libraries. All models are trained on Google Cloud Platform. Each model is tuned with learning rate, regularization (drop-outs), number of layers, tree depth as hyperparameters as applicable for respective models. The model is evaluated with 5-fold cross validation. The train and test data are split by the participant id. This is to ensure that the results on test data reflect the model performance on unseen participants. 


