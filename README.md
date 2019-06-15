# sequential_VAE

__Sequential VAE__ is a [variational autoencoder](https://arxiv.org/pdf/1312.6114.pdf) for sequential data -- 
in this case, sequences of characters. We use a [Gated Recurrent Unit](https://arxiv.org/pdf/1406.1078.pdf) 
to encode a tweet into a state vector. The state is linearly transformed into mean and variance vectors, from 
which we sample a latent vector `z`. This latent representation acts as the initial state of the decoder (also 
a GRU). Training consists of no discrete sampling, but does require feeding entire sequences to the decoder, 
whose job it is to predict character `t+1` given characters 1 through `t`, and initial state `z`. Then, at test 
time, the initial state is randomized, and each prediction is in turn concatenated back to the input, to 
generate wholly new sequences. 
