# Example model context: Rescorla–Wagner learning

This is a fictional teaching specification for a two-option task with binary rewards.
It combines a Rescorla–Wagner update with a softmax choice rule. It is one specified
variant, not a definition of every model called "Rescorla–Wagner".

Copy the model section into your practice project as `MODEL.md`. In a real project,
the scientist should write or verify the equations, conventions and test cases against
the intended method before asking an agent to implement them.

For background on this combination, see Wilson and Collins,
[Ten simple rules for the computational modeling of behavioral data](https://pmc.ncbi.nlm.nih.gov/articles/PMC6879303/).
The initial values and fitting bounds below are choices for this exercise.

## Question and data

Estimate how choices depend on learned reward values in a fictional two-option task.
Inputs are ordered rows with `session`, `trial`, `choice` and `reward`.
Choice is 0 or 1; reward is 0 or 1. Each session is fitted independently.
Reject missing fields, invalid values and duplicate session/trial pairs. Sort by trial
within session before evaluation.

## Equations and timing

Let Q_t(a) be the value of option a **before** choice t. At the start of each session,
Q_1(0) = Q_1(1) = 0.5.

Compute choice probabilities before using the reward from that trial:

```text
P(choice_t = a) = exp(beta * Q_t(a)) / sum_b exp(beta * Q_t(b))
```

Here beta is inverse temperature. After observing choice c_t and reward r_t:

```text
prediction_error_t = r_t - Q_t(c_t)
Q_(t+1)(c_t) = Q_t(c_t) + alpha * prediction_error_t
Q_(t+1)(a) = Q_t(a) for the unchosen option
```

The fitting objective is:

```text
negative_log_likelihood = -sum_t log P(choice_t = c_t)
```

For this exercise, fit by maximum likelihood with 0 <= alpha <= 1 and
0 <= beta <= 20. Use multiple starting points and report convergence and bound hits.
Compute log probabilities using a numerically stable formulation.

Do not add forgetting, separate positive/negative learning rates, perseveration,
lapse rates or participant-level pooling. Those would change the model.

## Checks specified before implementation

- With equal starting values, the first choice has probability 0.5.
- With alpha = 0, values never change.
- With beta = 0, each option has probability 0.5 on every trial.
- With alpha = 0.2, choosing option 0 and receiving reward 1 changes its value from
  0.5 to 0.6. The unchosen value remains 0.5.
- On the next trial with beta = 2, P(choice = 0) is approximately 0.549834.
- On the first two trials of that example, if both choices are option 0, the negative
  log likelihood is approximately 1.291286. The second reward must not change the
  probability assigned to the second choice.
- Starting a new session resets both values to 0.5.
- Invalid rows raise a useful error rather than being silently dropped.

Hand-check these cases independently of the implementation. Then assess parameter
recovery over a stated grid of parameters, several seeds and suitable trial counts.
Discuss tolerances before examining recovery results. At beta = 0, choices provide no
information about alpha; do not demand recovery of an unidentifiable parameter.

## Ask the agent to build the pipeline

```text
Read MODEL.md as the model specification. Identify ambiguities before coding.
Write tests from its hand-worked examples first. Then implement simulation,
likelihood evaluation, fitting and diagnostics as small functions.
Wire these into a script with a documented run command.
Keep synthetic observations in data/generated/.
Do not change the equations or expected values to get tests to pass.
After each coherent step, run the relevant tests, inspect the diff
and make a small, descriptive Git commit recording the check outcome.
```

Review the equations-to-code correspondence yourself. The agent can accelerate input
handling, fitting loops, tests, plots and run documentation. You remain responsible for
whether the specified model answers the scientific question.
