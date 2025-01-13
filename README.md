<div align="center">
<p align="center">
  <img src="assets/overall.jpg" width="50%" height="50%" />
</p>
</div>

<div align="center">
<h1>WebWalker: Benchmarking LLMs in Web Traversal</h1>
</div>

<div align="center">
<img src="https://img.shields.io/github/stars/alibabanlp/WebWalker?color=yellow" alt="Stars">
<a href=''><img src='https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Discussion-orange'></a>
<a href='https://huggingface.co/collections/callanwu/webwalkerqa-677f6527407edfda44098b09'><img src='https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Colloectionss-blue'></a>
<a href='https://huggingface.co/datasets/callanwu/WebWalkerQA'><img src='https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Datasets-green'></a>
<a href='https://huggingface.co/spaces/callanwu/WebWalkerQALeadeboard'><img src='https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Leaderboard-yellow'></a><br>
<a href='https://arxiv.org/pdf/2412.09501.pdf'><img src='https://img.shields.io/badge/Paper-arXiv-red'></a>

<!-- **Authors:** -->
<br>

_**Jialong Wu, Wenbiao Yin, Jiang Yong, Zhenglin Wang, Zekun Xi, Runnan Fang**_

_**Linhai Zhang, Yulan He, Deyu Zhou, Pengjun Xie, Fei Huang<br>**_

<!-- **Affiliations:** -->

_Tongyi Lab <img src="./assets/tongyi.png" width="14px" style="display:inline;">, Alibaba Group_

👏 Welcome to try web traversal via our **[<img src="./assets/tongyi.png" width="14px" style="display:inline;"> Modelscope online demo](https://www.modelscope.cn/studios/iic/WebWalker/)** or **[🤗 Huggingface online demo](https://huggingface.co/spaces/callanwu/WebWalker)**!

<p align="center">
<a href="https://alibaba-nlp.github.io/WebWalker/">[🤖Project]</a>
<a href="">[📄Paper]</a>
<a href="## 🚩Citation">[🚩Citation]</a>

</div>

Repo for [_WebWalker: Benchmarking LLMs in Web Traversal_]()

# 📖 Quick Start

- 🌏 The **Online Demo** is avaiable at [ModelScope](https://www.modelscope.cn/studios/jialongwu/WebWalker/) and [HuggingFace](https://huggingface.co/spaces/callanwu/WebWalker) now！

- 🤗 The **WebWalkerQA** dataset is avaiable at[ HuggingFace Datasets](https://huggingface.co/datasets/callanwu/WebWalkerQA)!

- 🤗 The **WebWalkerQA** Leaderborad is avaiable at[ HuggingFace Space](https://huggingface.co/spaces/callanwu/WebWalkerQALeadeboard)!

<img src="assets/demo.gif">

# 📌 Introduction

- We construct a challenging benchmark, **WebWalkerQA**, which is composed of **680** queries from four real-world scenarios across over **1373** webpages.
- To tackle the challenge of web-navigation tasks requiring long context, we propose **WebWalker**, which utilizes a multi-agent framework for effective memory management.
- Extensive experiments show that the WebWalkerQA is **challenging**, and for information-seeking tasks, **vertical exploration** within the page proves to be beneficial.

<div align="center">
    <img src="assets/method.jpg" width="80%" height="auto" />
</div>

# 📚 WebWalkerQA Dataset

The json item of WebWalkerQA dataset is organized in the following format:

```json
{
  "Question": "When is the paper submission deadline for the ACL 2025 Industry Track, and what is the venue address for the conference?",
  "Answer": "The paper submission deadline for the ACL 2025 Industry Track is March 21, 2025. The conference will be held in Brune-Kreisky-Platz 1.",
  "Root_Url": "https://2025.aclweb.org/",
  "Info": {
    "Hop": "multi-source",
    "Domain": "Conference",
    "Language": "English",
    "Difficulty_Level": "Medium",
    "Source_Website": [
      "https://2025.aclweb.org/calls/industry_track/",
      "https://2025.aclweb.org/venue/"
    ],
    "Golden_Path": ["root->call>student_research_workshop", "root->venue"]
  }
}
```

🤗 The WebWalkerQA Leaderboard is is avaiable at[ HuggingFace](https://huggingface.co/spaces/callanwu/WebWalkerQALeadeboard)!

You can load the dataset via the following code:

```python
from datasets import load_dataset
ds = load_dataset("callanwu/WebWalkerQA", split="main")
```

Additionally, we possess a collection of approximately 14k silver QA pairs, which, although not yet carefully human-verified.
You can load the silver dataset by changing the split to `silver`.

## 💡 Perfomance

### 📊 Result on Web Agents

The performance on Web Agents are shown below:

<div align="center">
    <img src="assets/agent_result.jpg" width="80%" height="auto" />
</div>

### 📊 Result on RAG-Systems

<div align="center">
    <img src="assets/rag_result.jpg" width="80%" height="auto" />
</div>

🤗 The WebWalkerQA Leaderboard is is avaiable at[ HuggingFace](https://huggingface.co/spaces/callanwu/WebWalkerQALeadeboard)!

🚩 Welcome to submit your method to the leaderboard!

# 🛠 Dependencies

```bash
conda create -n webwalker python=3.10
git clone https://github.com/alibaba-nlp/WebWalker.git
cd WebWalker
pip install -e .
# Install requirements
pip install -r requirement.txt
# Run post-installation setup
crawl4ai-setup
# Verify your installation
crawl4ai-doctor
```

### 💻 Running WebWalker Demo Locally

🔑 Before running, please export the OPENAI API key or Dashscope API key as an environment variable:

```bash
export OPEN_AI_API_KEY=YOUR_API_KEY
export OPEN_AI_API_BASE_URL=YOUR_API_BASE_URL
```

or

```bash
export DASHSCOPE_API_KEY=YOUR_API_KEY
```

> You can use other supported API keys with Qwen-Agent. For more details, please refer to the [Qwen-Agent](https://github.com/QwenLM/Qwen-Agent/tree/main/qwen_agent/llm). To configure the API key, modify the code in lines 42-51 of `src/app.py`.

Then, run the `app.py` file with Streamlit:

```bash
cd src
streamlit run app.py
```

### Runing RAG-System on WebWalkerQA

```bash
cd src
python rag_system.py --api_name [api_name]
--output_file [output_file]
```

The details of experiment settings can be found in the [readme file]() in the `src` folder.

# 🔍 Evaluation

The evaluation script for accuracy of the output answers using GPT-4o can be used as follows:

```bash
cd src
python evaluate.py --evaluate_file_path [path_to_output_jsonl_file]
```

## 🌻Acknowledgement

- This work is implemented by [ReACT](https://github.com/ysymyth/ReAct), [Qwen-Agents](https://github.com/QwenLM/Qwen-Agent), [LangChain](https://github.com/langchain-ai/langchain). Sincere thanks for their efforts.
- We sincerely thank the contributors and maintainers of [ai4crawl](https://github.com/unclecode/crawl4ai) for their open-source tool❤️, which helped us get web pages in a Markdown-like format.
- The repo is contributed by [Jialong Wu](https://callanwu.github.io/), if you have any questions, please feel free to contact via jialongwu@alibaba-inc.com or jialongwu@seu.edu.cn or create an issue.

## 🚩Citation

If this work is helpful, please kindly cite as:

```bigquery
@article{
}
```
