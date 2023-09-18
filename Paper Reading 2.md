# Paper Reading 2: BERT 
2023-08-16, Pre-training of Deep Bidirectional Transformers for Language Understanding

## BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding
I read this paper by the following sequence:  
1. Title + Authors
2. Abstract
3. Conclusion
4. Introduction
5. Related work
6. BERT Model
7. Experiments
### 1. Title + Author
The name BERT and ELMO are two characters in Sesame street.

### 2. Abstract 
BERT, short for Bidirectional Encoder Representations from Transformers, unlike previous pre-training works only applying unidirectional models, is the first bidirectional model in pre-training models, and it outperforms many tasks in absolute scores. BERT mainly has two pros:  
1. simple, generalized, powerful
2. Bidirectional

### 3. Conclusion
The BERT model describes itself as an integration of former works, including Trnasformer encoder, MLM, etc. And it is the first model to apply bidirectional architecture in pre-training tasks, making downstream tasks in QA and NSP more generalized and flexible.

### 4. Introduction
Still, intro part is the extension of the abstract. First, the paper reviews latest works concerning language model pre-training. There are two ways: sentence-level tasks and token-level tasks.

    (1) sentence-level tasks: natural language inferencee and paraphrasing, aiming at predict the relationships between sentences.
    (2) token-level tasks: named-entity recognition and question answering.

And there are two strategies for applying pre-trained to downstream tasks: feature-based and fine-tuning.  
    
    Feature-based: ELMo
    Fine-tuning: OpenAI GPT

Both have the same features:  
  1. they share the same objective function
  2. the are unidirectional

Then, the paper introduces BERT as a combination of sentence-level and token-level model using bidirectional architecture. To achieve bidirectional, BERT uses Transformer encoders and a technique called "masked language model"(MLM). Additionally, BERT also uses "next sentence prediction" for text-pair representations to capture the relationships between sentences.

Thus, BERT shows it powerful ability to mitigate the heavy tasks for task-specific architectures, and is the first pre-trained bidirectional model to achieve statee-of-the-art performance on both sentencee-level and token-leevel tasks.

### 5. Related work
The paper summerizes and reviews types of approaches that academics used in pre-training works. To learn more about the development of the area, one can go through papers if necessary.

### 6. BERT Model
Again, the most important part of DNN paper as to describe how the model or architecture is constructed.  
BERT, a model and a framework, consists of two parts: pre-training and fine-tuning.  

<font color=blue>Personal Thinking: Here we can see how abstract, introduction and models are related, from introduing pre-training, fine-tuning, bidirectional to the model itself.</font>  
    
    (1)Pre-training part: train the model on unlabeled data over different pre-training tasks. (generalization)
    (2)Fine-tuning part: for each downstream tasks, initializ parameters with the pre-trained ones; then train parameters with labeled data in each downstream task. (specification)

The construction of BERT is not complex, a multi-layer bidiectional Transformer encoders based on the <font color=red>original implementation</font> .

BERT<sub>BASE</sub> and BERT<sub>LARGE</sub> are proposed, the former is to compare with OpenAI GPT, and the latter is to show better grades. This perhaps initiates larger and larger models since it demonstrates the larger the model, the better the performance.

<font color=blue>Questions:  
  1.  how to compute the number of parameters in a BERT?</font>   

#### i. Input/Output
Next is BERT in details, input/output. Here, an input can be an arbitrary span of contiguous text. The input "sentence" does not need to be an actual linguisitic sentence, either a single sentence or a pair of sentences(e.g.,<question, answer>). A pair of sentences is packed in sequence by putting a special token [SEP] in between.  
The BERT input is constructed as follows:

    (1). First token is a special classification token [CLS], [CLS] is used for classification(NSP).
    (2). A [SEP] token is used between two sentences.
    (3). Words are represented as token embeddings.
    (4). The final input representation is the sum of three embeddings: the corresponding token embeddings(words), the segment embeddings(which sentence the word belongs to, simply 0 and 1 for two sentences) and the position embeddings(learnable, unlike Transformer's position encoding).

#### ii.Pre-trained BERT
The paper introduces Masked Language Model to construct a bidirectional model, and next sentence prediction to capture the relationships between two sentences.

Task 1: Masked Language Model(MLM)
    
    Mask some percentage of the input tokens at random with the [MASK] token and predict the masked words.

To mitigate the mismatch problem between pre-training and fine-tuning(the MLM does not appear in fine-tuning), BERT does the following during pre-training:  

    Choose 15% of random words, and replace the words with
    (1) the MASK token 80% of the time;
    (2) a random token 10% of the time;
    (3) the original word 10% of the time.

<font color=red>the probability 80%, 10%, 10% are based on experiment as the paper says.</font>  

Task 2: Next Sentence Prediction(NSP)  
The main idea is to capture <font color=red>relationships between sentences</font> so that BERT is able to complete tasks such as Question Answering and Natural Language Inference(NLI).
WHen implementing the NSP pree-training, choose sentence B is the actual sentence follows A 50% of the time, and 50% of the time B is a random sentence from the corpus(not the following sentence of A).

### 7. Experiments
The remaining chapters illustrate the detailed performence on different benchmarks.




