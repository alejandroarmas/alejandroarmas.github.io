+++
title = "Creating a Deep Learning Framework from Scratch in C++" 
author = "Alejandro Armas"
tags = ["Programming", "Mathematics"]
date = 2021-05-05
+++


My goal for this project was to train a simple 2-layer Multi-layer perceptron by creating a Deep Learning Framework. 

I gave myself the following restrictions:
1. Learn and incorporate as many design patterns and C++20 features as I could
2. Use little to no dependencies in my code

This is what a sample training loop might look like with my library:  

```c++
    constexpr double LEARNING_RATE = 0.001; 
    constexpr double TRAINING_EPOCS = 300; 

    auto ma = NeuralNetwork::Computation::Graph::TensorConstructor::create(
            Matrix::Rows(1), 
            Matrix::Columns(2000));
    
    auto ground_truth = NeuralNetwork::Computation::Graph::TensorConstructor::create(
            Matrix::Rows(1), 
            Matrix::Columns(10));
    

    NeuralNetwork::Sequential model;

    model.add(std::make_unique<NeuralNetwork::Layer>(
            std::make_unique<NeuralNetwork::MatrixMultiplyStep>(Matrix::Rows(2000), Matrix::Columns(1000)),
            std::make_unique<NeuralNetwork::AddStep>(Matrix::Columns(1000))    
    ));
    model.add(std::make_unique<NeuralNetwork::ActivationFunctions::ReLU>());
    model.add(std::make_unique<NeuralNetwork::Layer>(
            std::make_unique<NeuralNetwork::MatrixMultiplyStep>(Matrix::Rows(1000), Matrix::Columns(10)),
            std::make_unique<NeuralNetwork::AddStep>(Matrix::Columns(10))    
    ));
    
    auto CE = NeuralNetwork::Computation::Graph::TensorOp(Matrix::Operations::Metric::CrossEntropy{});

    for (int i = 0; i < TRAINING_EPOCS; i++) {
        auto out  = model.forward(ma);
        auto loss = CE(ground_truth, out);        
        loss->backwards();

        for (auto it = loss->parameters().begin(); it != loss->parameters().end(); ++it) {
            *it += -LEARNING_RATE * it.gradient();
        }

    }
```

### Results

I demonstrated my network improving via it's loss function, but I wanted more! I saw that Matrix Multiplication represented the majority of the neural network computation's runtime, so I found it was critical to optimize.

This project utilized parallel code via **OpenCilk**. It is a superset of C++ for parallel programming, hence the specialized compiler needed.

Here I profiled the elapsed time for a 25M parameter operation: 

[5000, 5000] x [5000, 5000] Parallel Matrix Multiply Benchmark: 6,831,126 ms.
[5000, 1] x [5000, 1] Cross Entropy Metric Benchmark: 34 ms.
[5000, 1] x [5000, 1] Outer Product Benchmark: 63,514 ms
[5000, 1] x [5000, 1] Softmax Benchmark: 5 ms
[5000, 1] x [5000, 1] Hadamard Product Benchmark: 21 ms.
[10000, 9000] Matrix Transpose Benchmark: 659166ms improved to 66771 ms.


In the end, I achieved a 142x and 10x speedup on MM and transpose ops by implementing Parallel Divide and Conquer algorithms and representing matrices in row-major order for reduced cache misses.

## Introduction

Typically representing models with a dynamic acyclic graph (DAG) provides a better user debugging experience, so data and calculations had to flow at runtime. 

## Design

I did this by encapsulating data in tensors, which were instantiated with a factory pattern and used in tandem with matrix operators, which were wrapped in a decorator object and together coupled with a global object to hold the graph’s edges. 

- Each node contains a statically built finite state automata, used in tandem with traversal policies, such as gradient descent to update state. 
- Additionally, iterator design patterns were used to decouple different traversal algorithms from the graph itself 

## Conclusion

This project came at a very personal time in my life. A lot of uncertainty was going on with my family, but I woke up every day programming to keep me going. I learned so much and used these learnings as I prepared for my next internship. 


<!-- ### Chain Rule

                DESCRIPTION:

Compute the gradients of each parent operand for each respective tensor. 

Recall the chain rule applied to vectorized gradients:
$$\frac{dJ}{dx} = \frac{dj}{dz} * \frac{dz}{dx}$$


There are three cases to consider:

Suppose we have the incoming gradient $\frac{dj}{dz}$ and we have $\vec{z}$ and $\vec{x}$, which are vectors in $R^n$ and $\bf{W}$ is a matrix in $R^{m*n}$

#### Case 1

$\vec{z} = \bf{W}\vec{x}$, where :
	
dj/dx = dj/dz * W
dj/dW = outerproduct{(dj/dz)^T, x^T}    


#### Case 2:

Now consider, $\vec{z} = \vec{x}\bf{W}$

dj/dx = dj/dz * W^T
dj/dW = outerproduct{x^T, dj/dz}

-->
