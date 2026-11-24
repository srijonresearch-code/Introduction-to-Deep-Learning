# Intro to Deep Learning

My notes and notebooks from Kaggle's **Intro to Deep Learning** course: building, training, and evaluating neural networks with TensorFlow and Keras.

## Topics Covered

- **The linear unit:** a single neuron computes `output = w1*x1 + w2*x2 + ... + b`. Weights set how much each input counts, and the bias shifts the result.
- **Deep networks:** stacking Dense layers in a `keras.Sequential` model, with hidden layers between the input and the output.
- **Activation functions:** ReLU adds the nonlinearity that stacked layers need. Without it, any number of linear layers collapses into one.
- **Training with SGD:** loss, gradient steps, learning rate, minibatches, and epochs. Adam is used as a good general-purpose optimizer.
- **Overfitting and underfitting:** reading training and validation loss curves, and using early stopping.
- **Dropout and batch normalization:** randomly switching off neurons so no neuron relies on a specific partner, which acts like training a committee of smaller networks.
- **Binary classification:** a sigmoid output layer, binary cross-entropy as the training loss, and accuracy as the reported metric.

## Worked Examples

- **Red wine quality (regression):** a network with 3 hidden layers of 512 neurons, trained on 11 scaled chemical measurements. Inputs were scaled to the range 0 to 1 using the training set's minimum and maximum only, so validation data could not leak into the scaling.
- **Binary classification:** a small network with a sigmoid output, trained with early stopping.

## Results

Validation results from my run of the binary classification example:

| | My run | Course reference run |
|---|---|---|
| Best validation loss | 0.60 | 0.35 |
| Best validation accuracy | 0.81 | 0.89 |

Same architecture, different numbers. Neural networks start from random weights and see batches in a random order, so two runs of identical code rarely match. A small validation set (about 100 rows) also makes each prediction worth about one percentage point of accuracy.

## Key Takeaways

- Neural networks need **scaled inputs**. A column with large numbers dominates the weighted sum and makes training unstable. Tree models like XGBoost did not have this problem.
- **Loss and accuracy do different jobs.** Cross-entropy changes smoothly as predictions improve, so the optimizer can train on it. Accuracy only changes when a prediction crosses the 0.5 line.
- Parameter counts are easy to check by hand. The wine network has `11*512+512 + 2*(512*512+512) + 513 = 531,969` parameters, far more than its ~1,100 training rows. That makes it prone to overfitting, which is why dropout and early stopping matter.
- Results vary between runs. Judge a model from several runs, not one.

## Tools & Libraries

`TensorFlow` · `Keras` · `pandas` · `matplotlib`

---
*Part of my self-directed path toward becoming a Machine Learning Engineer.*
