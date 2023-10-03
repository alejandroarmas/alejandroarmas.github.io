+++
title = "Resume"
description = "A background description of the author, Alejandro Armas"
date = "2023-06-20"
aliases = ["resume", "contact"]
author = "Alejandro Armas"
rootFontSize = "90%"
+++


## EXPERIENCE


### Ground Software Engineer Intern | Aug 2022 – Nov 2022
##### [Astranis Space Technologies](https://www.astranis.com) | San Francisco, CA

-  Enhanced satellite comms by redesigning backend app, React frontend, and proprietary event processor. The
modifications ensured idempotent writes into Elasticsearch, significantly reducing satellite noise for operators.
-  Improved the resiliency of Kubernetes deployments by re-engineering all software micro-services to pull configurations
upon pod startup. This modification resulted in a reduction in system downtime, leading to more reliable operations

### Software Developer Intern | Mar 2021 – Nov 2021
##### [Exploratory Systems Laboratory](https://resilientdb.com/#team) | Davis, CA

- Enhanced the accessibility and usability of ResilientDB, our blockchain distributed system, by spearheading an initiative to
extend its toolkit and develop comprehensive core documentation, as evidenced by 79 stars and 141 forks on GitHub.
- Launched the [ExpoBlog](https://blog.resilientdb.com/about.html), hosting 22 insightful posts and reducing the on-boarding of colleagues from months to weeks.
- Designed and developed RESTful API endpoints for decentralized application data store connectivity

### Research Scientist Intern | May 2020 - Aug 2020 
##### [Massachusetts Institute of Technology - Biology Summer Research Program](https://biology.mit.edu/program-details-bsg-msrp-bio/) | Remote, CA
-   Investigated the underpinnings which confer advantages to reinforcement learning algorithms; where learning a distribution of cumulative sum of discounted rewards, is advantageous to merely learning its expected value.
-   Implemented quantile regression loss function and back-propagation algorithms to learn underlying data distributions.
-   Trained Agents in OpenAI’s Gym Atari environments using Deepmind’s Acme and Reverb, connecting remotely through the OpenMind Computing Cluster to perform GPU accelerated workloads.

### Intern - Interdisciplinary and Quantitative Biology REU |  Jun. 2019 - Aug. 2019 
##### [Universidad de Puerto Rico, Rio Piedras](https://iqbioreu.uprrp.edu/index.php/2019-cohort/) | San Juan, Puerto Rico
- Achieved meaningful results by using k-means clustering and ggplot2, tidyr, and tibble to cluster Lassioglassum malachurum by locomotor activity, providing biologists with an automated categorization of large scale bee experiments that replaced manual sorting.
- Assisted in writing contributions to supervisor’s thesis, presented weekly to colleagues, and created blog posts to document lab procedures; effectively communicating research findings to a variety of audiences.
## PROJECTS

### Traffic Prediction Service (Request Access for View) | May 2023 - Present
**Tech: Ray, Docker, Terraform, DVC, S3, ONNX, Plotly**
- Enabled reproducible data analysis by leveraging DVC to capture data lineage, provisioning both object storage and IAM
policies using Terraform for secure access, optimizing network transfers by 35x and packaging notebooks via Docker

### [some-dl-models](https://github.com/alejandroarmas/some-dl-models) | Jan 2023 - Apr 2023
**Tech: PyTorch, comet ml, Poetry, ONNX, Github Actions**
-   Developed ML platform and integrated Comet ML to log training metrics and persist ONNX model artifacts, achieving an increased experimentation workflow.
- Tested algorithms such as CNN, LSTM and GNN to achieve successful outcomes on CIFAR, Pubmed and Reddit datasets.
- Enforced common development environment on local machines, using Poetry as a package manager and pre-commit hooks such as Black, Mypy, Flake8, unit testing and conventional commits, accelerating development feedback loops.
-   Streamlined the PR process by leveraging Github actions to automate linting, static analysis and unit-testing, resulting in improved code quality.

### [MLOPS Question + Answer Bot](https://alejandroarmas.github.io/post/sf-llm-stack-hackathon/) | Mar 2023 - Mar 2023
**Tech: Relevence AI, Redis, OpenAI**
- Developed a LLM pipeline for Q/A using Redis Vector Search, achieving 2nd place at MLOps.community LLM SF Hackathon

### [Automatic Differentiation Backpropagation Engine](https://github.com/alejandroarmas/Wirikuta) | Dec. 2021 - Jun. 2022
**Tech: C++20, C++17, C++14, OpenCilk, doctest, Catch2**
-   Constructed engine to dynamically build directed acyclic graphs of tensors and computational operations at runtime. Each node contains a statically built finite state automata, for traversal policies such as gradient descent.
-   Achieved **142x speedup** over naive Matrix Multiply and **10x speedup** on transpose operations by implementing Parallel Divide and Conquer algorithms and representing matrices in row-major order for reduced cache misses.

### [D-Cash Wallet Web Server](https://github.com/alejandroarmas/gunrock_web) |  May 2021 - Jun. 2021    
**Tech: C++, Stripe API, RapidJSON, POSIX threads, Git**
- Developed secure server wallet authentication, transfer, deposit, and charge issuance services, with integration of Stripe API.
- Implemented consumer-producer multi-threaded client request concurrent processing scheme to improve latency.


### Davis In-Order CPU | Mar 2021 - Jun 2021
**Tech: Chisel, Scala, RISC-V, Python, Pandas and Matplotlib**
- Developed a comprehensive RV32I Pipelined CPU design using Chisel HDL, incorporating several functional units such as
Branch Predictor, Hazard Unit, Forwarding Unit, ALU, ALU Control Unit, and Control Unit.
- Conducted extensive simulations and analysis comparing the performance of single-cycle and pipelined designs. Utilized
four different branch predictors and varied saturation bits over six workloads to create detailed visualizations.

### [Lineage-based Data Store](https://github.com/p3terlo/lstore_db) | Jan 2021 - Apr 2021
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

**Libraries:** NumPy, PyTorch, Pandas, Matplotlib, OpenCilk, doctest, Catch2, RapidJSON, Acme, Reverb, Gym


### Honors and Achievements
**Professional Memberships**:
- Scholar, NSF LSAMP/CAMP program at UC Davis 		(June 2021 - 2022)
- Scholar, AvenueE - VIP Research Program 			(June 2021 - 2022)
- Member, Artificial Intelligence Society at UC Davis 		(Jan 2020 - Jan 2021)
- Member, NSF LSAMP/CAMP program at UC Davis 		(Dec 2019 - June 2021)
- Member, UC Davis AvenueE 2019 Cohort (1 of 30 students) 	(Sept 2019 - 2022)
- Member, Institute of Electrical and Electronics Engineers (IEEE)

**Awards, Grants and Fellowships**:
- UC Davis ECE Undergraduate Travel Grant ($500)
- AvenueE Travel Grant ($500)
- ABRCMS Student Travel Award ($685.57)
- UC Davis AvenueE Scholarship ($10500)
- EOPS Perpetual Spirit Scholarship ($1000)
- LMC Academic Competition scholarship ($500)
- AvenueE Scholar Award ($1000)
- LMC Academic Honors Spring 2019
- LMC Dean's List 2017-2019
