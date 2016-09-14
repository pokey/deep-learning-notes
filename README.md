- Weight initialization
  - [Random walk initialization for training very deep feedforward
    networks](http://arxiv.org/abs/1412.6558) **(preferred)**
    - View deep network as random walk on logs of norms of vectors
    - Rescale weight matrices to make walk unbiased
    - Used by http://arxiv.org/abs/1511.03771
  - For RNNs
    - [iRNN](https://arxiv.org/abs/1504.00941)
      - Initialize weight matrix between hidden states to identity to avoid
        vanishing / exploding gradients
      - [uRNN paper](http://arxiv.org/abs/1511.06464) claims that it doesn't
        work very well:

        > We found the IRNN to be particularly unstable; it only ran without
        > blowing up with
        > incredibly low learning rates and gradient clipping. Since the
        > performance was so poor relative to
        > other models we compare against, we do not show IRNN curves in the
        > figures.
    - [npRNN](http://arxiv.org/abs/1511.03771)
      - Modify idea of iRNN by initializing with random positive definite
        matrix with all eigenvalues <=1
      - Claims improved performance
- Architecture
  - Nonlinearity
    - ReLUs **(preferred)**
    - tanh is more popular for RNNs
  - RNNs
    - [LSTM](http://deeplearning.cs.cmu.edu/pdfs/Hochreiter97_lstm.pdf) **(preferred)**
      - [tutorial](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
    - [uRNN](http://arxiv.org/abs/1511.06464)
      - Enforces that weight matrix has eigenvalues all identically 1
      - Does this by decomposing transition matrices and making them
        complex-valued
      - Seems intriguing to force matrices to be unitary by design, but
        unsatisfyingly complicated solution.  Feels like there should be a
        simpler way
      - [code](https://github.com/amarshah/complex_RNN)
      - [interesting discussion on reddit](https://www.reddit.com/r/MachineLearning/comments/3uk2q5/151106464_unitary_evolution_recurrent_neural/)
  - [Batch normalization](http://arxiv.org/abs/1502.03167) **(preferred)**
    - Renormalizes the outputs from each layer to save higher layers from
      having to constantly learn the variances of the layers below
    - Defines *Internal Covariate Shift*
    - Allows much higher learning rates and less careful initialization of
      parameters
    - [Applied to RNNs](http://arxiv.org/abs/1603.09025)
- Regularization
  - [Dropout](http://jmlr.org/papers/volume15/srivastava14a/srivastava14a.pdf)
    **(preferred)**
    - Randomly turn off nodes during training, and rescale output during
      testing
    - Extremely simple yet effective form of regularization
    - [Applied to RNNs](http://arxiv.org/abs/1603.05118)
  - L2 weight decay
  - [Batch normalization](http://arxiv.org/abs/1502.03167) claims to be a form
    of regularization, though they still seem to use L2 in addition
- Learning algorithm
  - Adaptive learning rate
    - RMSProp **(preferred)**
    - [ESGD](http://arxiv.org/abs/1502.04390) *(promising)*
      - Alternative preconditioner trying to attach saddle points
    - [AdaGrad](http://www.magicbroom.info/Papers/DuchiHaSi10.pdf)
  - Momentum **(preferred)**
    - TODO: More info
- Tricks
  - Grid search on learning rate and dropout percentage
    - Used in [npRNN](http://arxiv.org/abs/1511.03771)
- RNNs (TODO: fill out more, referencing above papers)
  - Vanishing / Exploding gradients
    - [The problem](http://www-dsi.ing.unifi.it/~paolo/ps/tnn-94-gradient.pdf)
    - [Orthogonal RNNs](http://arxiv.org/abs/1602.06662)
      - Explicitly constructs RNN solutions to 2 common toy problems
      - Uses this to understand why iRNNs vs orthogonal RNN work well for some
        tasks
      - Introduces something that mixes between them
    - Parameter initialization (iRNN, npRNN)
    - Architecture (uRNN)
    - Gradient clipping
    - LSTM
    - 3 approaches described in iRNN paper
      - Optimization algorithm
