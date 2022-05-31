- [Profiler](https://www.tensorflow.org/guide/profiler)
- [Optimising your input pipeline performance with tf.data](https://towardsdatascience.com/optimising-your-input-pipeline-performance-with-tf-data-part-1-32e52a30cac4)
- [Data Paralell](https://www.tensorflow.org/guide/data_performance)
- Naive Approach
![image](https://user-images.githubusercontent.com/64508435/171122698-87916fcc-6102-42c1-918b-3e4be80c02e1.png)

This diagram shows that a training step includes opening a file, fetching a data entry from the file and then using the data for training. We can see clear inefficiencies here as when our model is training, the input pipeline is idle and when the input pipeline is fetching the data, our model is idle.
- Prefetching
