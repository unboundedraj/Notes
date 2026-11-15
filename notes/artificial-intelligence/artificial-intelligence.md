---
title: Artificial Intelligence
date: 2026-11-05
tags: [ai, intelligence, artificial intelligence]
---

## What is Artificial Intelligence?

Artificial Intelligence (AI) is a branch of computer science that enables machines and computers to perform tasks that normally require human intelligence, such as learning, problem-solving, decision-making, and understanding language. AI uses technologies like Machine Learning and Deep Learning to analyze data, identify patterns, and make predictions. Some common examples of AI are ChatGPT, Google Assistant, Siri, self-driving cars, and facial recognition systems. AI is widely used in education, healthcare, banking, business, and transportation to save time, improve efficiency, and reduce human effort. In simple words, Artificial Intelligence makes machines smart enough to perform tasks that usually require human intelligence.

## What is Machine Learning?

Machine Learning (ML) is a branch of Artificial Intelligence (AI) that enables computers and machines to learn from data and improve their performance without being explicitly programmed for every task. It uses algorithms to analyze data, identify patterns, make predictions, and take decisions based on previous experiences. Machine Learning is mainly divided into three types:  
**Supervised Learning, Unsupervised Learning, and Reinforcement Learning.**  
Some common examples of Machine Learning include email spam detection, product recommendations on Amazon, movie recommendations on Netflix, fraud detection in banking, and voice recognition. It is widely used in healthcare, education, business, finance, and many other industries. In simple words, **Machine Learning allows computers to learn from data and improve their performance automatically**.

## What is Supervised Learning?

**Supervised Learning** is a type of Machine Learning in which a computer or machine learns from labelled data, where both input and correct output are already provided. The model is trained using this data to understand patterns and make predictions or decisions when new data is given. Supervised Learning is mainly divided into two types: Classification and Regression. Classification is used to predict categories, while Regression is used to predict numerical values. Common examples include email spam detection, house price prediction, disease prediction, and exam result prediction. In simple words, Supervised Learning means training a machine using input data along with the correct answers so that it can predict accurate results for new data.

### **What is Classification?**

**Classification** is a type of Supervised Machine Learning in which a model predicts or categorizes data into predefined classes or categories. It learns from labelled data and identifies patterns to classify new data into the correct category.

**Examples:**

- Email classification as Spam or Not Spam.
- Predicting whether a person has a disease or not.
- Classifying an image as a Cat or Dog.
- Predicting whether a customer will buy a product or not.

**In simple words:** Classification is used when we want to predict a category or class.

### **What is Regression?**

**Regression** is a type of Supervised Machine Learning in which a model predicts continuous numerical values based on input data. It learns from existing data and identifies relationships between variables to predict numerical outcomes.

**Examples:**

- Predicting house prices.
- Predicting a student's marks.
- Predicting monthly sales.
- Predicting temperature.

**In simple words:** Regression is used when we want to predict a numerical value.

## What is Unsupervised learning?

**Unsupervised Learning** is a type of Machine Learning in which a model learns from unlabelled data, meaning the input data is provided without any predefined output or correct answers. The model independently analyses the data, identifies hidden patterns, discovers similarities, and groups similar data points together. Unsupervised Learning is mainly divided into two techniques:   
**Clustering and Association.**   
Common examples include customer segmentation, grouping similar products, and analysing shopping patterns. It is widely used in marketing, business, banking, and data analysis. In simple words, Unsupervised Learning allows machines to find hidden patterns and relationships in data without human-provided labels

### **What is Clustering?**

**Clustering** is a type of Unsupervised Machine Learning in which a model groups similar data points together based on their features or characteristics without using labelled data. It identifies hidden patterns and similarities in the dataset and creates different groups called clusters. Common examples include customer segmentation, grouping similar news articles, and grouping customers based on purchasing behaviour. In simple words, Clustering means dividing data into different groups based on similarities.

### **Types of Clustering**

1. **K-Means Clustering:** Divides data into a predefined number of clusters based on similarity.
2. **Hierarchical Clustering:** Creates clusters in a tree-like structure by grouping similar data points.
3. **DBSCAN Clustering:** Groups closely packed data points and identifies outliers or noise.
4. **Mean Shift Clustering:** Groups data points based on the density of data.

### What is association?

**Association** is a technique of Unsupervised Machine Learning used to discover relationships and patterns between different items in a dataset. It identifies which items frequently occur together and helps understand the buying behaviour or interests of customers. A common example is Market Basket Analysis, where a supermarket finds that customers who buy bread often also buy butter or milk. Association is widely used in retail, e-commerce, and marketing to recommend products and improve sales. In simple words, Association helps machines discover which items or events are frequently connected to each other.

## What is Deep Learning?

Deep learning is a branch of machine learning that uses artificial neural networks with many layers (hence “deep”) to learn patterns directly from data.

**The core idea**

A neural network is made of layers of simple units called neurons. Each neuron takes inputs, multiplies them by weights, adds them up, and passes the result through a non-linear function. Stack many such layers and the network can model very complex relationships. During training, the network makes predictions, measures how wrong they are using a loss function, and adjusts its weights through backpropagation and gradient descent to reduce that error. Repeat this over millions of examples and the weights settle into something useful.

**What makes it different from traditional machine learning**

In classical machine learning, a human often designs the features by hand, for example edge detectors for images or word counts for text. In deep learning, the early layers learn simple features (edges, textures, word fragments) and later layers combine them into higher-level concepts (faces, sentence meaning). The network learns the features itself, which is why it works so well on raw, unstructured data.

**Common architectures**

- **CNNs (convolutional neural networks):** images and video
- **RNNs and LSTMs:** sequences like time series and older speech or text models
- **Transformers:** the dominant architecture today for language, and increasingly for images, audio, and more. Large language models like Claude are built on this
- **GANs and diffusion models:** generating images and other media

### **Where it’s used**

Image recognition, speech-to-text, machine translation, recommendation systems, chatbots, self-driving perception, medical imaging, fraud detection, and more.

**Trade-offs**

Deep learning usually needs large datasets and significant compute (GPUs/TPUs), and its models can be hard to interpret. For small tabular datasets, simpler methods like gradient-boosted trees often perform as well or better.

**How it relates to the other terms**

AI is the broad goal of building intelligent systems, machine learning is the approach of learning from data, and deep learning is the subset of machine learning that uses multi-layer neural networks.

## What is an agent with respect to AI?

An AI agent is a system that uses an AI model, usually a large language model, to pursue a goal on its own by deciding what to do, taking actions, and adjusting based on what happens. A plain chatbot answers a question and stops. An agent keeps going until the task is done.

**The core loop**

Most agents run some version of this cycle:

1. **Perceive:** take in the goal and the current state (user request, files, tool outputs, earlier results)
2. **Reason and plan:** decide what to do next, often breaking the goal into steps
3. **Act:** call a tool, such as running code, searching the web, querying a database, sending an email, or calling an API
4. **Observe:** read the result of that action
5. **Repeat** until the goal is met or the agent decides it needs help

### **What an agent is made of?**

- **A model** that does the reasoning and decides on actions
- **Tools** that let it affect the world beyond generating text
- **Memory or context** to track what it has done so far, within a task and sometimes across tasks
- **Instructions and guardrails** that define its goal, limits, and when to ask a human for approval

**A simple example**

Ask a chatbot “why is my test failing?” and it will guess from what you paste in. A coding agent will open the repository, run the tests, read the error, edit the code, rerun the tests, and repeat until they pass. Claude Code works this way.

**Agent vs. workflow**

A workflow follows a fixed, predefined sequence of steps, even if some steps use an LLM. An agent chooses its own steps dynamically. Workflows are more predictable and cheaper. Agents are more flexible but harder to control and can make mistakes that compound over many steps.

**Multi-agent systems**

Sometimes several agents work together, for example one that plans, one that writes code, and one that reviews it. This can help with large tasks but adds complexity.

**Trade-offs**

Agents can handle open-ended, multi-step work, but they can be slower, costlier, and less reliable than a single well-designed prompt. Because they take real actions, they usually need permission limits and human oversight for anything risky or irreversible.
