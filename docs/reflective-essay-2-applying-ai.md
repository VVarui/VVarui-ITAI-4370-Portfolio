# Reflective Essay 2: Applying AI to Telecommunications Problems

*[Edit this draft to reflect your own voice and experience before submitting — it's written from the labs' content, but the reflection should be genuinely yours.]*

Across the labs, I applied several different AI and machine learning approaches to telecom problems, and one of the biggest lessons was that "the right model" depends entirely on the problem's structure, not on which model is newest or most sophisticated.

In Lab 3, I used a Random Forest to predict hourly network traffic and found that a single feature — traffic from one hour ago — accounted for over 80% of the model's predictive power. That was a useful, humbling result: it would have been easy to build an elaborate model, when in fact the network's recent history did most of the work. It taught me to check feature importance early, rather than assuming complexity equals accuracy.

Lab 4 pushed this lesson further. I compared ARIMA, a feature-engineered linear regression, and an LSTM neural network on the same forecasting task. The linear regression returned a suspiciously perfect R² of 1.0000, which at first looked like a success — until I recognized it as a sign of data leakage, likely from a moving-average feature that had access to information it shouldn't have had. Diagnosing that gave me more confidence than if the model had simply "worked": I learned to treat too-good-to-be-true results as a debugging trigger rather than a reason to celebrate. The LSTM's more modest but believable error (RMSE ≈ 18 Mbps) turned out to be the more trustworthy result of the three.

Lab 5 applied AI to a different kind of telecom problem: not predicting the network, but running efficiently *within* it. Compressing a cloud-trained IoT classification model through pruning, quantization, and distillation showed me that AI deployment isn't just about training a good model — it's about matching a model's footprint to the hardware it will run on. The finding that pruning slightly *improved* accuracy while cutting the model's size by nearly three-quarters was, for me, the single most important result in the whole course: it reframed compression not as a compromise, but sometimes as an improvement.

Together, these labs showed me that applying AI to telecommunications is less about picking a powerful algorithm and more about understanding the problem's constraints — data structure, time-dependence, hardware limits — and choosing (or building) the model that respects them.
