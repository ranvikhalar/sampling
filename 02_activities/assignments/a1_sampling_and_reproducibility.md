# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 100 (from the original 1000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: Ranveer Kaur

```
**bold Sampling for Infection**
Sampling Frame - 1000 (wedding - 200 + brunches - 800)
Sample Size - 100 (exactly 10% of people at every event are infected. wedding sample - 20 and brunches sample - 80)
Sampling Procedure - Stratified Random Sampling Without Replacement
Function - np.random.choice where replace=False
Distribution - Binomial distribution with p = 0.10. However, the sampling is without replacement and the independent condition does not meet.

**bold Sampling for Tracing (primary contact tracing)**
Sampling Frame - Number of Infections, 100
Sample Size - A proportion of the infected individuals, determined by TRACE_SUCCESS = 0.20
Sampling Procedure - Simple Random Sampling. Randomly assigning numbers between 0 and 1.
Distribution - Bernoulli distribution

**bold Sampling for Tracing (secondary contact tracing)**
Sampling Frame - Individuals traced in the primary contact tracing step.
Sample Size - event_trace_counts = ppl[ppl['traced'] == True]['event'].value_counts()
Sampling Procedure - Purposive Sampling (two infections are independently traced to the same source event)
Function - events_traced = event_trace_counts[event_trace_counts >= SECONDARY_TRACE_THRESHOLD].index
           ppl.loc[ppl['event'].isin(events_traced) & ppl['infected'], 'traced'] = True

**bold Relation to blog post** - The code models the observations in the blog post about infections, contact tracing with primary and secondary steps. 
```

```
The graph obtained from the code is not same as in the blog post. The frequency for the Proportion of cases for Traced to Weddings histogram overlaps more to the Infections from Weddings histogram comparing to the graph in the blog post. 

```
```
After running the code multiple times for 100 repetitions, the graph changes everytime because the random functions generate different results eveytime. 

```

```
By setting the random seed, the code will produce same results for each run. The addition of np.random.seed(42) will produce the same graph every time.

```


## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Altercation of the code|The code changes made, made it reproducible.|The code is still not reproducible.|
|Description of changes|The author explained the reasonings for the changes made well.|The author did not explain the reasonings for the changes made well.|

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `23:59 - 16/02/2025`
* The branch name for your repo should be: `assignment-1`
* What to submit for this assignment:
    * This markdown file (a1_sampling_and_reproducibility.md) should be populated.
    * The `whitby_covid_tracing.py` should be changed.
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sampling/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `assignment-1`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via the help channel in Slack. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
