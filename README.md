# FineSurE: Fine-grained Summarization Evaluation using LLMs



The structure of the projects:
- dataset: FRANK and REALSumm (in JSON format) are located in this folder
- reproduce: the code to reproduce the results of FineSurE in Table 1 and Table 2 
- finesure: the code to run our FineSurE method to evaluate the summary generated from language models

## Highlight

**FineSurE** is a *multi-dimensional*, *fine-grained* automated evaluation framework for text summarization. It covers there distinctive evaluation dimensions, namely faithfulness, completeness, and conciseness. These dimensions are crucial to assess the capability of modern language models in summarization, as they are susceptible to incorrect statement, information omission, and verbosity.

FineSurE framework breaks down a complicate evaluation process into ```two simple human-like evaluation tasks``` using LLMs. 

- **Fact Checking:** This is a task of solving a categorization problem involving nine categories. These include the seven factuality errors, along with an additional category "other error" for error outside the seven errors, and an additional category "no error" for cases whether no error was detected. Given a pair of input text and model summary, the LLM is expected to output the error type classified into one of the nine categories for each sentence along with a concise reason.
  
- **Keyfact Alignment:** This is an alignment task of matching each keyfact into the summary sentences from which the keyfact is inferable. Given a pari of keyfact list and model summary, the output should be the binary label (whether inferable or not) an dth elist of line numbers of all summary sentences matched for each keyfact.


## Running FineSurE on Model Summareis

We take sample datasets with 10 examples for fact-checking and keyfact-alignment tasks, respectively.

Please replace the ```openai api key``` with your api key in ```finesure/fact-checking.py``` and ```finesure/keyfact-alignmnet.py```.

#### Runnining Command:
```bash
cd CodeRelease
python finesure/fact-checking.py [input-path] [output-folder]

# example code for fact checking on sampled data.
python finesure/fact-checking.py dataset/frank/frank-data-sample-10.json result/fact-checking
```

#### Runnining Command:
```bash
cd CodeRelease
python finesure/keyfact-alignment.py [input-path] [keyfact-path] [output-folder]

# example code for keyfact alignment on sampled data.
python finesure/keyfact-alignment.py dataset/realsumm/realsumm-data-sample-10.json dataset/realsumm/human-keyfact-list.json result/keyfact-alignment
```

#### Logs:

The results are saved in the result directory. See the results on examples below:

* Fact Checking Task:
```bash 
[Evaluation Results]
* sentence-level factuality error ratio per model (lower is better)
bert_sum	0.0%
bus	33.3%
pgn	16.7%
s2s	83.3%
bart	33.3%

* summary-level faithfulness score per model (higher is better)
bert_sum	100.0%
bus	66.7%
pgn	83.3%
s2s	16.7%
bart	75.0%

* system-level model ranking (left is better)
['bert_sum', 'pgn', 'bart', 'bus', 's2s']

* success rate: 100.0%
```

* Keyfact Alignment Task:
```bash 
[Evaluation Results]

* completeness score per model (higher is better)
unilm_out_v2	45.5%
t5_out_large	59.0%

* completeness model ranking (left is better)
['t5_out_large', 'unilm_out_v2']

* conciseness score per model (higher is better)
unilm_out_v2	76.0%
t5_out_large	81.7%

* conciseness model ranking (left is better)
['t5_out_large', 'unilm_out_v2']

* success rate: 100.0%
```

## Reproduce the Main Table of the model

```bash
cd CodeRelease/reproduce
python reproduce-main-results.py results/frank-result-by-gpt4-w-finesure.json results/realsumm-result-by-gpt4-w-finesure.json
```


## Author

Adarsh Srivastava

Computer Science and engineering

National Institute of Technology, Patna (NITP)

[Github profile](https://github.com/adarsh-2011)           [Linkdin](https://www.linkedin.com/in/adarsh-srivastava-10a783257/)

## contact

For any query please feel free to reach out me at [srivastavaadarsh434@gmail.com](mailto:srivastavaadarsh434@gmail.com)
