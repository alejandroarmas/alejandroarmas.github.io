+++
title = "Resume"
description = "A background description of the author, Alejandro Armas"
date = "2023-06-20"
aliases = ["resume", "contact"]
author = "Alejandro Armas"
rootFontSize = "90%"
+++


<!-- 
\begin{center}
    \textbf{\Huge \scshape Alejandro Armas} \\ \vspace{1pt}
    \small 1+(925) 470-6873 $ |$ \href{mailto:armas@ucdavis.edu}{\underline{armas@ucdavis.edu}} $ |$ 
    \href{https://alejandroarmas.github.io}{\underline{alejandroarmas.github.io}}
    \href{https://linkedin.com/in/armasalejandro/}{\underline{linkedin.com/alejandro}} $ |$
    \href{https://github.com/alejandroarmas}{\underline{github.com/alejandro}}
\end{center} -->

## EXPERIENCE


### Intern - Ground Software | Aug. 2022 – Nov. 2022
##### Astranis Space Technologies | San Francisco, CA

- Dramatically decreased satellite noise for satellite operators by modifying back-end application, react frontend, and
in-house event streaming processor to ensure idempotent writes into Elasticsearch.
- Enhanced system resiliency by revising all software services and leveraging Kubernetes to pull configurations on pod
startup.
### Intern - MIT Summer Research Program | May 2020 - Aug. 2020 
##### Massachusetts Institute of Technology | Remote, CA
-   Investigated the underpinnings which confer advantages to reinforcement learning algorithms; where learning a distribution of cumulative sum of discounted rewards, is advantageous to merely learning its expected value.
-   Implemented quantile regression loss function and back-propagation algorithms to learn underlying data distributions.
-   Trained Agents in OpenAI’s Gym Atari environments using Deepmind’s Acme and Reverb, connecting remotely through the OpenMind Computing Cluster to perform GPU accelerated workloads.

### Intern - Interdisciplinary and Quantitative Biology REU |  Jun. 2019 - Aug. 2019 
##### Universidad de Puerto Rico, Rio Piedras Rio Piedras, Puerto Rico
- Achieved meaningful results by using k-means clustering and ggplot2, tidyr, and tibble to cluster Lassioglassum malachurum by locomotor activity, providing biologists with an automated categorization of large scale bee experiments that replaced manual sorting.
- Assisted in writing contributions to supervisor’s thesis, presented weekly to colleagues, and created blog posts to document lab procedures; effectively communicating research findings to a variety of audiences.
## PROJECTS

### Traffic Prediction Service (Request Access for View) | May 2023 - Present
**Tech: Ray, Docker, Terraform, DVC, S3, ONNX, Plotly**
- Enabled reproducible data analysis by leveraging DVC to capture data lineage, provisioning both object storage and IAM
policies using Terraform for secure access, optimizing network transfers by 35x and packaging notebooks via Docker

### [some-dl-models](https://github.com/alejandroarmas/some-dl-models) | Jan. 2023 - Apr. 2023
**Tech: PyTorch, comet ml, Poetry, ONNX, Github Actions**
-   Developed ML platform and integrated Comet ML to log training metrics and persist ONNX model artifacts, achieving an increased experimentation workflow.
- Tested algorithms such as CNN, LSTM and GNN to achieve successful outcomes on CIFAR, Pubmed and Reddit datasets.
- Enforced common development environment on local machines, using Poetry as a package manager and pre-commit hooks such as Black, Mypy, Flake8, unit testing and conventional commits, accelerating development feedback loops.
-   Streamlined the PR process by leveraging Github actions to automate linting, static analysis and unit-testing, resulting in improved code quality.

### [Automatic Differentiation Backpropagation Engine](https://github.com/alejandroarmas/Wirikuta) | Dec. 2021 - Jun. 2022
**Tech: C++20, C++17, C++14, OpenCilk, doctest, Catch2**
-   Achieved **142x speedup** over naive Matrix Multiply and **10x speedup** on transpose operations by implementing Parallel Divide and Conquer algorithms and representing matrices in row-major order for reduced cache misses.
-   Constructed engine to dynamically build directed acyclic graphs of tensors and computational operations at runtime. Each node contains a statically built finite state automata, for traversal policies such as gradient descent.

### [D-Cash Wallet Web Server](https://github.com/alejandroarmas/gunrock_web) |  May 2021 - Jun. 2021    
**Tech: C++, Stripe API, RapidJSON, POSIX threads, Git**
- Developed secure server wallet authentication, transfer, deposit, and charge issuance services, with integration of Stripe API.
- Implemented consumer-producer multi-threaded client request concurrent processing scheme to improve latency.


### [Lineage-based Data Store](https://github.com/p3terlo/lstore_db) | Jan. 2021 - Apr. 2021
**Tech: Python, Git**
-   Oversaw team of 5 programmers, partitioned responsibilities, led meeting agendas and oversaw implementation of multi-version hybrid OLTP/OLAP database management system with novel QueCC concurrency protocol.
-   Spearheaded performance critical development: in-memory record indexing and system memory management.
-   Mediated system design for concurrency control, contention-free lazy record consolidation and data durability.
-   Demonstrated and encouraged use of version control, unit-testing and best coding practices.
## TECHNICAL SKILLS

**Relevant Coursework:** 
- [Performance Engineering for Software Systems](https://www.ece.ucdavis.edu/~jowens/)
- [Deep Learning](http://www.ifmlab.org/courses_ecs189g_2022.html)
- [(Social) Fairness of Machine Learning Algorithms](https://github.com/ucdavis/FairMLCourse/blob/main/README.md)
- [Distributed Database Systems](https://expolab.org/ecs265-fall2021.html)
- Computer Architecture


**Skills:** C/C++20, Python, Rust, R, Risc-V, JavaScript, SQL (sqlite, postgres), {{< katex "\LaTeX" true />}}, CSS, Markdown, HTML, Bash, Spanish Developer Tools: Kubernetes, Docker, Terraform, S3, EC2, Git, Azure, Github Actions, Github Codespaces, Ably

**Libraries:** OpenCilk, doctest, Catch2, RapidJSON, NumPy, PyTorch, Pandas, Matplotlib, Acme, Reverb, Gym

