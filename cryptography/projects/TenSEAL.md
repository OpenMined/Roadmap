# TenSEAL

_Last modified: February 5th, 2020_

## Introduction

At the heart of every deep learning framework is a tensor object (e.g vectors and matrices). Neural networks implementation invloves a lot of matrix multiplication, addition, slicing etc. In order to be able to build a deep learning framework capable of dealing with encrypted data, someone need to have a tensor type capable of handling encrypted data and evaluating the same operations native tensors do (e.g multiplication).

## Overview

TenSEAL aims to provide an efficient tensor type that holds encrypted data using homomorphic encryption (HE) techniques. It should also be possible to evaluate basic operations required by neural networks on this tensor type. We will initially use the [CKKS](https://eprint.iacr.org/2016/421.pdf) scheme for encryption, this scheme is already implemented in the [SEAL](https://github.com/Microsoft/SEAL) library which we rely on extensively. The project is implemented in C++ and provide a binding for Python.

The project is decomposed of three main part that we describe next:

#### Simple Tensor Type
This step aims at providing a first simple tensor type which doesn't use batching capabilities of the CKKS scheme, this will make it unefficient compared to what batching provide, however, this will help in experimenting with the library and testing integration with deep learning frameworks.

#### Provide Linear Approximation for Most Used Functions
Oftentimes we use low degree polynomials to approximate non-linear functions, those polynoms can be expressed as circuits with gates representing multiplication and addition operations. When doing homomorphic encryption, we really care about the size of the circuit (the number of gates), we want to keep it as minimal as possible. This part is about building optimized circuits for specific low degree polynomial.

#### Efficient Tensor Type
This is not already defined, as an efficient and generic HE tensor type hasn't been proposed yet, this is more like experimentation/implementation iterations. The main idea is to structure the tensor in a way that we can use the batching functionality of the CKKS scheme, it basically allow to perform a single instruction on multiple data. Finding the best structure for an HE tensor is key to make homomorphic encryption practical in deep learning.
