# Reflective Essay 2: Applying AI to Telecommunications Problems

Across the labs, I applied several different AI and machine learning approaches to telecom problems, and one of the biggest lessons was that "the right model" depends entirely on the problem's structure.

In Lab 3, I used a Random Forest to predict hourly network traffic and found that a single feature accounted for over 80% of the model's predictive power.The results showed that would be easier to build an elaborate model. It taught me to check feature importance early, rather than assuming complex equals accuracy.

In Lab 4, I compared ARIMA, a feature-engineered linear regression, and an LSTM neural network on the same forecasting task. The linear regression returned a suspiciously perfect R² of 1.0000, which at first looked like a success until I found it as a sign of data leakage, likely from a feature that had access to information it shouldn't have had. The LSTM's more modest but believable error (RMSE ≈ 18 Mbps) turned out to be the more trustworthy result of the three.

In Lab 5, I applied AI to a different kind of telecom problem: not predicting the network. Compressing a cloud-trained IoT classification model through pruning, quantization, and distillation showed me that AI deployment is about matching a model's footprint to the hardware it will run on. 

Together, these labs showed me that applying AI to telecommunications is less about picking a powerful algorithm and more about understanding the problem's constraints.
