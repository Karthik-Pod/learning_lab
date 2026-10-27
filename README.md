# learning_lab

My practice space for the technical skills of my MSc in Artificial Intelligence
(Human-Centered Intelligent Systems) at Radboud University.

Each area gets its own folder with a topic guide and my practice work.
Every area is built on its own branch and merged through a pull request,
so I practise the team workflow all the time.

## How I learn a topic

1. **Learn** – read the topic explanation or watch the linked resource
2. **Try it** – do the practice steps myself, typing every command
3. **Struggle** – stuck? Try 15 minutes alone, then ask for help
4. **Explain** – write a short entry in [LEARNING_LOG.md](LEARNING_LOG.md)

A topic is done when I can do it **without looking at the guide**.

---

## Topics

Work top to bottom: later areas build on earlier ones.

### 1. Git & GitHub → [`01-git-github`](01-git-github/README.md)
- [ ] Repositories and the 4 places (working folder, stage, local, remote)
- [ ] Staging and committing
- [ ] Reading history and changes
- [ ] Branches
- [ ] Merging
- [ ] Merge conflicts
- [ ] Undoing mistakes
- [ ] Remotes: push, pull, fetch
- [ ] `.gitignore`
- [ ] Stash
- [ ] Pull requests and code review
- [ ] Issues and linking work
- [ ] Forks
- [ ] Keeping a branch up to date in a team
- [ ] Good commit messages

### 2. Terminal & Linux
- [ ] Navigating folders and files
- [ ] Running programs, arguments, environment variables
- [ ] Pipes and searching (`|`, `grep`)
- [ ] SSH into a remote machine (for compute clusters)
- Resource: [The Missing Semester](https://missing.csail.mit.edu/)

### 3. Python for research
- [ ] Project structure: modules and packages
- [ ] Virtual environments and `requirements.txt`
- [ ] Writing a small command-line tool
- [ ] Type hints and docstrings
- [ ] Testing with `pytest`

### 4. Working with data
- [ ] Logging experiment data cleanly (CSV / JSON per participant)
- [ ] pandas: loading, cleaning, grouping
- [ ] Plotting results (matplotlib)

### 5. Statistics for user studies
- [ ] Within- vs between-subjects designs, counterbalancing
- [ ] t-tests and effect sizes
- [ ] Mixed-effects models (`statsmodels`)
- Resource: *Discovering Statistics* (Andy Field)

### 6. Math for ML
- [ ] Linear algebra: vectors, matrices, matrix products
- [ ] Probability: distributions, Bayes' rule, expectation
- [ ] Derivatives and gradients
- Resource: *Mathematics for Machine Learning* (free book), ch. 2, 5, 6

### 7. Deep learning from scratch
- [ ] Backpropagation by hand (micrograd)
- [ ] A small language model (makemore)
- [ ] The same in PyTorch
- Resource: Karpathy, *Neural Networks: Zero to Hero*

### 8. ML evaluation & experiments
- [ ] Train / validation / test splits, data leakage
- [ ] Baselines and metrics
- [ ] Significance of results
- [ ] Experiment tracking (Weights & Biases or MLflow)

### 9. Probabilistic modelling
- [ ] Bayesian inference
- [ ] Building models in PyMC
- Resource: *Statistical Rethinking* (McElreath), ch. 1–9

### 10. Robotics with ROS2
- [ ] Nodes, topics, messages
- [ ] Controlling a simulated robot

### 11. Reading research
- [ ] Three-pass paper reading
- [ ] 3-line summaries of my target supervisor's papers

### 12. Specialisation (pick one, later)
- [ ] Active inference · neuroAI · mechanistic interpretability

---

## Rules

1. One topic at a time.
2. Type the code and commands myself. AI explains, I build.
3. Courses come first; pause in busy weeks.
4. Every area: branch → practise → PR → merge → tick the box → log entry.
