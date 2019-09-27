X033524: Statistical Learning and Inference
Final Project Readme File
Author: Simona Emilova Doneva

The submitted files in 'code and data' folder contain the code to reproduce the results reported in the final report.

NOTE: one has to include the original train.csv and test.csv files in the code and data folder (they were excluded due to size limitations for the upload)

The code files are in Jupyter format.
Prerequisites for running the notebooks:
- python version 3.6.3
- jupyter: https://jupyter.org/install

Libraries:
- sklearn version 0.20.1
- pandas version 0.23.4

The notebooks contain the following. They can be directly re-run:

1. Baselines Generation
- references to used information for the models
- loading of the data
- for each model (KNN, LR, LDA, SVM): 
	- a pipeline is created that consists of: standardization step, model definition
	- the pipeline is fit on the whole train data set
	- generate_predictions_file() is called to produce the submission file which was then evaluated on kaggle
- generate_predictions_file(): gets as input the trained model, the test data as pandas data frame and the desired file name to store
	
2. Dimensionality Reduction
	2.1. Optimal value range for the number of components estimation
- split of the original train data into train and validation set. Since the files could not be uploaded due to the size and the split procedure is random, the exact results reported in the report might be slightly different.
- benchmark_pca_variance(): loops over different variance values to obtain by PCA and calls benchmark_pca() for each value. 
- benchmark_pca(): for a given variance value to obtain computes the number of components to keep, 
reduced the data based on that number, trains and evaluates the model 
- visualise_benchmark(): produces the graphs on the model performance with different number of components

	2.2. Optimal value for number of components with Cross Validation
- evaluate_pca_pipeline_cv(): for a given model (KNN, LR, LDA, SVM) and given range of values for the number of PCA components: 
	- a pipeline is created that consists of: standardization, PCA, model definition
	- a parameter grid is defined from the given range
	- 5-fold CV is executed, the optimal results are printed out and a plot is generated
- for each model based on the estimated range, the method above is executed to find the optimal number of components

	2.3. Visualisations
- the train data is projected with PCA and LDA both keeping the first two components

	2.4. Predictions Generation
- the same function generate_predictions_file() described earlier is called to produce the results for final evaluation

3. Hyperparameters Tuning
	3.1. A <model name>_param_selection() function is defined for each model. This function describes a CV procedure to fine-tune
the model specific parameters. It returns the best parameters setting and the best obtained score.
	3.2. Predictions generation (see above, this time the models are initiated with the fine-tuned parameters)

4. Further Experiments
- PCA+LDA for dimensionality reduction experiment
- QDA: includes parameters fine tuning

5. L1 vs L2 Regularization Visualisation (visualisation in the report)
