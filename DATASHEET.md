# Datasheet: BBO Capstone Query History Dataset

## 1. Motivation

This dataset was created to support my Black-Box Optimisation (BBO) capstone project. The purpose of the dataset is to record the query points I submitted for each of the eight unknown functions, together with the scalar outputs returned by the capstone portal.

The dataset supports a **sequential optimisation task**: each new round uses the accumulated query-output history to decide the next point to test. Its main role is therefore not general prediction, but iterative decision-making under a strict evaluation budget.

### Why the dataset was created
- to track the full optimisation history across rounds
- to support week-by-week query selection
- to make the optimisation process transparent and reproducible
- to document how my strategy evolved as more data became available

## 2. Composition

The dataset contains:
- **8 optimisation problems**
- input vectors with dimensionality from **2D to 8D**
- one scalar output for each submitted query
- cumulative weekly history across rounds

Each function has a different input dimensionality:
- Function 1: 2D
- Function 2: 2D
- Function 3: 3D
- Function 4: 4D
- Function 5: 4D
- Function 6: 5D
- Function 7: 6D
- Function 8: 8D

The stored data consists of:
- the query vectors submitted to the portal
- the returned scalar outputs
- round-by-round accumulated history

### Data format
- numeric input vectors in `[0,1]`
- scalar floating-point outputs
- grouped by function and round

### Known gaps and limitations in composition
- the true underlying functions are unknown
- no gradients or calibrated uncertainties are available
- the sampled points are not uniformly distributed across the space
- later rounds are concentrated around previously successful local regions
- higher-dimensional functions remain sparsely explored relative to their search volume

## 3. Collection Process

The dataset was collected through repeated interaction with the capstone project portal over multiple weekly rounds.

### How new data points were generated
In each round:
1. I reviewed the full query-output history so far.
2. I identified whether each function appeared to be:
   - still improving,
   - plateauing,
   - or drifting away from an earlier best region.
3. I selected one new query point per function.
4. I submitted those query points through the portal.
5. I recorded the returned scalar outputs.
6. I appended the new data to the cumulative history.

### Strategy used across time
The query strategy changed as the dataset grew:
- **Early rounds:** broader exploration and rough region-finding
- **Middle rounds:** cautious local refinement around high-performing regions
- **Later rounds:** stronger exploitation for stable improvers, with resets toward earlier best points when recent drift underperformed

So the dataset is **adaptive and policy-dependent**, not a neutral or random sample of the search space.

### Time frame
The dataset was collected over the capstone project across multiple weekly submission rounds.

## 4. Preprocessing and Uses

### Preprocessing applied
I did not apply heavy preprocessing to the stored query-output pairs.

The main transformations were organisational:
- grouping results by function
- tracking best-so-far values
- comparing local query directions over time
- summarising trends such as improvement, plateauing, or regression

The raw submitted queries and returned outputs were preserved as the core dataset.

### Intended uses
This dataset is intended for:
- supporting the next round of black-box optimisation
- analysing how the optimisation strategy evolved over time
- documenting decision-making in a low-budget sequential search problem
- reflecting on optimisation assumptions, limitations, and biases

### Inappropriate uses
This dataset should **not** be used as:
- an unbiased benchmark sample of the full search space
- a general supervised-learning training set with strong external validity
- evidence that unexplored regions are low-value
- proof of global optimality for any function

Because the query process is adaptive, the dataset becomes increasingly concentrated around regions that already looked promising.

## 5. Distribution and Maintenance

### Availability
The dataset is stored in my BBO capstone GitHub repository as part of the project’s experiment history and documentation.

### Terms of use
This dataset is intended for **educational and capstone purposes**. It reflects a course-based optimisation workflow and should be interpreted in that context.

### Maintenance
The dataset is maintained by me as the repository author.

Maintenance includes:
- appending each weekly round of submitted queries and returned outputs
- preserving round-by-round history
- updating documentation when the strategy changes
- correcting formatting issues if needed

### Versioning approach
The most important form of versioning is the **round-by-round history**, since each round adds new information and may change the optimisation strategy.

## 6. Assumptions Embedded in the Dataset

This dataset reflects several assumptions made during collection:
- local improvement is often a useful signal for the next step
- promising nearby regions are worth refining further
- later rounds can shift toward exploitation once stronger regions have been identified
- a limited number of evaluations means broad global coverage is less realistic over time

These assumptions shape the dataset directly, because they influence which areas were sampled and which were left unexplored.

## 7. Potential Biases and Risks

The main bias in the dataset is **sampling bias introduced by the optimisation strategy itself**.

Examples:
- later rounds are concentrated near previously successful points
- some functions received repeated local refinement while other parts of the domain remained untouched
- higher-dimensional spaces are underexplored relative to their size

This means the dataset should be interpreted as a **trace of an optimisation policy**, not a balanced or representative dataset of all possible inputs.

## 8. Why This Datasheet Matters

This datasheet is useful because it makes clear that the BBO query history is not just a collection of numbers. It is the result of a sequence of decisions, assumptions, and strategy changes.

Documenting those choices helps:
- make the optimisation process easier to follow
- improve reproducibility
- clarify how the data was shaped by the search strategy
- prevent overclaiming what the dataset can support

In that sense, the datasheet is not just about the data itself, but also about the reasoning that produced it.
