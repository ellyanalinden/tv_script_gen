# TV Script Generation

## Table of Contents
* Project description
* Development Tools
* Discussion
* Result and Conclusion
* References

## Project description
Generate TV scripts using RNN and LSTM

## Development Tools
* PyTorch Framework

## Discussion
1. I followed the lecture from Udacity DLND for the hyperparameters as a starting point.
2. Inital batch_size was 128 with sequence_length = 100, learning rate of 0.01, hidden_dim = 215. There was error message 'RuntimeError: cuda runtime error (59) : device-side assert triggered at /opt/conda/conda-bld/pytorch_1524584710464/work/aten/src/THC/generic/THCStorage.c:36'.
3. I change the batch_size to 64 with sequence_length = 5, lr of 0.01, hidden_dim = 215. The model's losses increased from 5.8 (first loss) to 6.9 and the loss numbers after that were around 6-7 during training. The model didn't seem to learn.
4. I changed hidden_dim to 128. The losses were around 5.
5. I changed the sequence_length to 10. The losses were still around 5.
6. I changed the lr to 0.001. The losses decreased to 4.3, however, during training, the losses bounced around 4.3-4.1
7. I changed the batch_size to 100, sequence_length: 5, and with 20 epochs. The losses decreased gradually from 5.11 to 3.8 (the last epoch). I think I am heading to the right direction. I increased the epochs number to 50 for the next training.
8. I changed the embedding_dim to 50, as the previous dimension (300) resulted in very slow loss decreasing. This didn't work.
9. I used embedding_dim 200 and increased the clipping rate from 5 to 15. Epoch: 30. Loss at the last epoch: 3.7 and the loss reduced too slow.
10. I increased the clipping rate to 20 to speed up the training. It didin't work. I just found out that I had bugs with my dropout layer.
11. I solved the problem after 32 hours training (attempting different hyperparameters), trying to discover why the losses decreased so slow.

## Result & Conclusion
Aim loss is 3.5
To achive that, I used:
1. clipping rate : 10
2. no of words in a sequence: 10
3. batch size: 100
4. 10 epochs
5. learning rate: 0.001
6. embedding dim: 200
7. hidden dim: 256
8. number of RNN layers: 2
<br />
Last epoch's loss is 3.25

## References
* https://datascience.stackexchange.com/questions/31109/ratio-between-embedded-vector-dimensions-and-vocabulary-size 
* https://www.quora.com/How-do-I-determine-the-number-of-dimensions-for-word-embedding 
* https://www.quora.com/What-is-word-embedding-in-deep-learning 
* https://pytorch.org/tutorials/intermediate/char_rnn_generation_tutorial.html
* Udacity Deep Learning Nanodegree Program
