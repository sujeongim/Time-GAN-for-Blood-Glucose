# Codebase for "Time-series Generative Adversarial Networks (TimeGAN)", for Blood Glucose Level Data

This directory is a partial modification of the the original TimeGAN code to allow TimeGAN to be also applied to blood glucose data.

Original Paper: Jinsung Yoon, Daniel Jarrett, Mihaela van der Schaar, 
"Time-series Generative Adversarial Networks," 
Neural Information Processing Systems (NeurIPS), 2019.

Authors: Jinsung Yoon, Daniel Jarrett, Mihaela van der Schaar

Paper Link: https://papers.nips.cc/paper/8789-time-series-generative-adversarial-networks

Contact for code : sujeongim@postech.ac.kr

## Data

- Used Data
   - Bloog Glucose Level Data of 20 Virtual T1DMS Patients 
   
-  Data for original Time-Series GAN
    -   Sine data: Synthetic
    -   Stock data: https://finance.yahoo.com/quote/GOOG/history?p=GOOG
    -   Energy data: http://archive.ics.uci.edu/ml/datasets/Appliances+energy+prediction


## TimeGAN Tutorial

To run the pipeline for training and evaluation on TimeGAN framwork, simply run 
python3 -m main_timegan.py or see jupyter-notebook tutorial of TimeGAN in tutorial_timegan.ipynb.

Note that any model architecture can be used as the generator and 
discriminator model such as RNNs or Transformers. 

## Code explanation

(1) data_loading.py
- Transform raw time-series data to preprocessed time-series data (Googld data)
- Generate Sine data

(2) Metrics directory
  (a) visualization_metrics.py
  - PCA and t-SNE analysis between Original data and Synthetic data
  (b) discriminative_metrics.py
  - Use Post-hoc RNN to classify Original data and Synthetic data
  (c) predictive_metrics.py
  - Use Post-hoc RNN to predict one-step ahead (last feature)

(3) timegan.py
- Use original time-series data as training set to generater synthetic time-series data

(4) main_timegan.py
- Report discriminative and predictive scores for the dataset and t-SNE and PCA analysis

(5) utils.py
- Some utility functions for metrics and timeGAN.

### Command inputs:

-   data_name: BG level(=Blood Glucose Level), sine, stock, or energy (we mainly used BG level)
-   seq_len: sequence length
-   module: gru, lstm, or lstmLN
-   hidden_dim: hidden dimensions
-   num_layers: number of layers
-   iterations: number of training iterations
-   batch_size: the number of samples in each batch
-   metric_iterations: number of iterations for metric computation

Note that network parameters should be optimized for different datasets.

### Example command

```shell
$ python3 main_timegan.py --data_name bg_level --seq_len 24 --module gru
--hidden_dim 24 --num_layer 3 --iteration 50000 --batch_size 128 
--metric_iteration 10
```

### Outputs

-   ori_data: original data
-   generated_data: generated synthetic data
-   metric_results: discriminative and predictive scores
-   visualization: PCA and tSNE analysis
