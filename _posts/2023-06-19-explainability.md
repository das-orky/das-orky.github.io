---
layout: single
classes: wide
author_profile: false
sidebar:
  nav: "foo_all"
header:
  overlay_image: /assets/images/post_explainability_1.jpg
  caption: "(CC) chenspec"
title: "Explainable AI (XAI)"
excerpt: >
  Explaining the reason behind an output from a neural network can make the network more trustworthy, and can understand its internal representation.<br />
categories:
  - Genomics
tags:
  - peak calling
  - neural network
  - explainability
---

# Why Explain?


Deep Neural Network has become such a vital apparatus of A.I that, now both the terms are almost synonyms of each other. While deep learning networks have been shown to be effective in a variety of applications, most have not seen the light of production for consumers. This is because many of these systems lack explainability, or the ability to explain how they arrived at their decisions. This lack of explainability can make it difficult for users to trust and rely on these systems, especially in critical applications. The term explainability and interpretability are used interchangeably. 
{: .text-justify}
Explainability is the ability to understand the reasons behind an outcome. For example, if a loan is denied, it is important to be able to explain why the decision was made. Similarly, if someone is predicted to develop Alzheimer's in the next 20 years, it is important to be able to explain the basis for the prediction. This ability to explain the output makes the result more trustworthy and understandable.
{: .text-justify}

Cows on the Beach: A machine learning [model](https://arxiv.org/pdf/1807.04975.pdf) was trained to identify cows. When an image of a cow near a beach was input to the model, it failed to detect the cow. This is because the model was trained on a dataset of images that mostly showed cows in lush green fields or in cowsheds. The model learned to associate cows with these backgrounds, and so it did not recognize the cow in the beach image.
{: .notice--danger}
{: .text-justify}

![cows on the beach](/assets/images/post_explainability_2.jpg){: .align-center}

# Ways To Explain

Some machine learning algorithms are inherently interpretable, but deep neural networks are not. They work like a black box, meaning that it is difficult to understand how they make their predictions. However, there are post-hoc analysis techniques that can be used to interpret deep neural networks. 

The type of explanation that is needed for a particular problem depends on the nature of the problem. For example, in image classification, a small perturbation in the input image may not change the class of the image. Therefore, the explanation for an image classification model does not need to be sensitive to small changes. However, in genome analysis, a single nucleotide change can change the classification of the genome. Therefore, the explanation for a genome analysis model needs to be sensitive to small changes. The explainability method must be an accurate proxy of the model’s decision-making process and be comprehensible to humans[1] 
{: .text-justify}

There are a variety of techniques available to make neural network models explainable. The landscape of ideas for doing so can be summarized as follows [1]:

![various explainability approaches](/assets/images/post_explainability_3.jpg){: .align-center}


Global explainability techniques are used to understand the overall model and its working. These techniques, such as permutation importance, partial dependence plots, and accumulated local effects, can help to identify the most important features and how they contribute to the model's predictions. Local interpretability techniques, on the other hand, are good at finding features in the input that can positively or negatively impact the decision of the model. These techniques can be used to understand why a particular prediction was made and to identify potential biases in the model.
{: .text-justify}

There are two prominent ways to do local explaination:

* Input Perturbation
* Analysing gradient backpropagation   

Input perturbation is a technique for explaining the predictions of a machine learning model by perturbing the input values and observing the effect of this change on the network and the output. This technique can be computationally expensive, as it requires multiple passes through the network to converge to an explanation . Gradient-based approaches, on the other hand, are more efficient, as they only require a single pass (forward and backward) through the network to calculate the attribution. In gradient-based approaches, the attribution is calculated with respect to the backpropagation values of the features or the input. In gradient based approach propagating the probabilities backward distributes the responsibility of the decision over the input features. This can also be done in game theoretic way by finding the shapely values between the backward propagating probabilistic values and the input features for a layer.
{: .text-justify}

Nonlinearity is an essential component of neural networks. However, it can make it difficult to monitor the input-output relationship, as nonlinear layers (such as ReLU) can saturate input values. One way to mitigate this effect is to find a baseline or reference input for the input data. This can be challenging for some problems, but for images, it can be as simple as initializing all pixels to black or white, or with some random values. 
{: .text-justify}

In the case of DNA, finding a baseline for an input is not straightforward. The question that needs to be asked is, "What am I interested in measuring differences against?"[2] There are also some characteristics of DNA that need to be considered, such as the fact that CG content is underrepresented. Therefore, the baseline cannot simply be random nucleotides.
{: .notice--danger}
{: .text-justify}

# To Sum It Up

PyTorch has some great support for explainable AI.

![to sum it up](/assets/images/post_explainability_5.jpg){: .align-center}

# Explainability And Genomics

Explainable AI (XAI) is essential for the field of AI, as changes in even a single nucleotide can have a significant impact on gene expression. XAI can help to ensure that AI models are equitable and trustworthy, and can build trust between researchers, clinicians, and patients. This can improve patient care, as clinicians can use XAI to trace out more accurate diagnostic pathways for patients.
{: .text-justify}

The first layer of a neural network is typically responsible for learning low-level features. If the network is not performing well, visualizing the first layer can help us to identify problems with the way that the network is learning features. By understanding how the network learns features, we can make changes to the network architecture or the training process that can improve the performance of the network. Visualizing the first layer can help us to understand how the network is learning to identify different nucleotides and its pattern. The code used in this post can be found in [this](https://github.com/das-orky/Explainability) github repository. 
{: .text-justify}

To visualize the first layer of a trained neural network, one must first extract the weights of that layer.
```python
def cnn_layers_property(model):
    
    model_layers=list(model.children())
    cnn_layer_weights=[]
    cnn_layers=[]
    cnn_layer_bias=[]
    for i in range(len(model_layers)):
        if type(model_layers[i]) == nn.Conv1d:
            cnn_layers.append(model_layers[i])
            cnn_layer_weights.append(model_layers[i].weight)
            cnn_layer_bias.append(model_layers[i].bias)

    return cnn_layer_weights, cnn_layer_bias, cnn_layers
  ```

The code will take as input a pytorch model, with layers of Conv1d. It will return three values, weights of all the Conv1d layers, its associated biases and the layers. With this information plotting of the filter weights can be done. Remember in this example only filter weights of the first layer will be plotted. That is, 0th index of the weight matrix of the model. 

```python
def show_cnn_filters(cnn_layers_weight):
    
    columns=8
    rows=int(np.ceil(cnn_layers_weight[0].shape[0]/columns))
    filter_width=cnn_layers_weight[0].shape[2]
    layer_weight=cnn_layers_weight[0]

    plt.figure(figsize=(20,17))

    for i, filter in enumerate(layer_weight):
        ax=plt.subplot(rows,columns,i+1)
        ax.imshow(filter.cpu().detach(),cmap='gray')
        ax.set_yticks(np.arange(4))
        ax.set_yticklabels(['A','C','G','T'])
        ax.set_xticks(np.arange(filter_width))
        ax.set_title(f"Filter{i}")

    plt.tight_layout()
    plt.show()
```

# How Filters React To An Input

When an input (positive or negative) is given to a convolutional neural network (CNN), the filters in the first layer react to it by highlighting the features that are relevant to the classification task. If the input data is labeled, we also happen to know the pattern that makes the input positive or negative. By looking at the output of the first layer, we can expect to see a pattern in the filter output that is consistent (more or less) with the known pattern. If this pattern is consistent across all the positive data sets, then we can say that the first layer is learning something relevant to the classification task.
{: .text-justify}

To understand the patterns that the filters are learning, it is necessary to extract the weights of the input data after it has passed through the first layer. The weights of the input data are a representation of the features that the filters are learning to identify. A function is needed that takes as input a genome and passes it through the trained model's first layer.  
{: .text-justify}

```python
# Pass the data through the 1st layer. 
def genome_to_weights(genome,cnn_layer):

    with torch.no_grad():
        genome=genome.to(device,dtype=torch.float32)
        weights=cnn_layer(genome)
        return weights
```

Giving as input all the positive sequences, so that their weights can be generated for the first layer.

```python
weights=[]
for genome,_ in positive_test_data_raw:
    genome_one_hot=torch.stack([torch.tensor(dna_to_one_hot_encoding(genome))])
    weights.append(genome_to_weights(genome_one_hot,cnn_layers[0]))
```

After all the positive sequences have been passed through the first layer, the weight vector of all the sequences is stored. This vector contains both positive and negative values, where the negative values may negatively impact the final outcome of the input. To simplify the analysis, we can set a threshold of keeping only the values greater than zero in the vector, and discarding the rest. This will give us a vector of only positive values, which we can then use to identify which nucleotide is represented by each positive value. Once we have identified the nucleotides, we can create a positional weight matrix, which will show the weightage of each nucleotide at each position. This helps us to understand which nucleotides are more important at each position in the sequence.
{: .text-justify}

```python
def create_pwm(weights,positive_test_data_raw,cnn_layers):
    filter_width=cnn_layers.kernel_size[0]
    
    pwm=np.zeros((cnn_layers.out_channels,cnn_layers.in_channels,filter_width),dtype=int)
    for i,weight in enumerate(weights):
        for filter_idx in range(cnn_layers.out_channels):
            above_thresh=torch.where(weight[0][filter_idx] > 0)[0]
            for j in above_thresh:
                pwm[filter_idx]=pwm[filter_idx] + dna_to_one_hot_encoding(positive_test_data_raw[i][0][j:j+filter_width])
            
    return pwm 
```
After getting the positional weight matriz and the weights of the first layer, it is time to plot them side by side. The code is given in [this](https://github.com/das-orky/Explainability) repository


![filter layer one](/assets/images/post_explainability_4.jpg){: .align-center}


While the positional weight matrix may appear random in this example, it is important to remember that this is just a proof of concept. In a real experiment, where there is a definite outcome and we expect to see some pattern of a regulatory element, the positional weight matrix may show the underlying pattern in a vague way. This is because the positional weight matrix is only the first layer of the model, and the higher layers may be able to better identify the pattern. However, even the first layer can be helpful in understanding that the model is trained in the right direction.
{: .text-justify}

# Interpreting Model One Input At A Time

For a particular input, we want to know which part of the input plays a positive or negative role in forming the outcome. To understand this, one can use many explanation models mentioned above, such as Shap, DeepLift, and DeepLiftShap. However, many of these AIX methods require a baseline set of input. It is not trivial to find a baseline input for a DNA input. Techniques like saliency maps do not require a baseline to calculate the attribution. In the example below, the baseline for DeepLiftShap and DeepLift is a set of four input sequences, where in each sequence only one nucleotide is active. This is not ideal, as it ignores the interactions between nucleotides. Please read Ways To Explain topic above. Below are the output of Saliency, DeepLift and DeepLiftShap. It seems random, but please use the code in the [notebook](https://github.com/das-orky/Explainability) to know how to use these techniques in your real experiments. 
{: .text-justify}

![Model Interpretation](/assets/images/post_explainability_6.jpg){: .align-center}



[1]https://arxiv.org/pdf/2107.11400.pdf

[2]https://arxiv.org/pdf/1704.02685.pdf