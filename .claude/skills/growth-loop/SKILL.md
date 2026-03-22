---
name: growth-loop
description: Experiment cycle for any project. Checks metrics, declares winners, proposes new experiments. Use when reviewing or managing growth experiments.
disable-model-invocation: true
context: fork
---

Experiment cycle. Hypothesis → test → measure → learn → repeat.

## Karp Loop Integration

For bounded mutation loops (web performance, landing page optimisation, code
quality), use the Karp Loop harness at ~/dev/products/elixir/karp_loop/.

Karp Loop needs 5 things to start: objective, surface, evaluator, budget, decision.
If any are missing, do not start the loop — propose the missing pieces in queue.md.

To start a Karp Loop experiment:
```bash
KARP_LOOP_CONFIG=config/<experiment>.json bash ~/dev/products/elixir/karp_loop/scripts/run_loop.sh
```

To check status:
```bash
KARP_LOOP_CONFIG=config/<experiment>.json bash ~/dev/products/elixir/karp_loop/scripts/status.sh
```

Adjutant's role: decide WHAT to experiment on, write the config, monitor status.
Karp Loop's role: run the iterations, verify, repair, keep/discard.

## For Simple Experiments (no Karp Loop)

For A/B tests and metric checks that don't need the full harness:

## Step 1: Orient

Read the project file (knowledge/projects/[project].md) and experiment files
(experiments/_active.md + any per-experiment files for this project).

What experiments are running? What's their status? What metrics do we have?

## Step 2: Measure

For each running experiment:
- Check the metric source (PostHog, Google Analytics, gws, or whatever
  the experiment file specifies)
- Record today's measurement in the experiment file
- Has it reached the decision criteria (days elapsed OR statistical significance)?

## Step 3: Decide

For experiments that reached decision criteria:
- Declare a winner with evidence
- Move the experiment to experiments/_results.md with the learning
- Remove from experiments/_active.md
- Append to queue.md: "Urgent | growth-loop | [Project] experiment concluded..."
- If the winner needs to be made permanent (deploy, update config), create
  an Action Required item in queue.md

For experiments still running:
- Log today's data point
- If stalled >48hrs with no new data, flag in queue.md

## Step 4: Learn

After processing all experiments, review experiments/_results.md for patterns:
- What's working across projects?
- What's consistently failing?
- Are there adjacent hypotheses suggested by the data?

Update the project file with any strategic insights.

## Step 5: Propose

If fewer than 2 experiments are active for this project, propose a new one:
- Write a hypothesis based on learnings from past experiments
- Define the metric, baseline, target, and decision criteria
- Create a new experiment file in experiments/
- Add to experiments/_active.md
- Append to queue.md: "Action Required | growth-loop | New experiment proposed..."

The experiment is proposed, not started. Adjutant (main agent) reviews and
either approves or adjusts before deployment.

## Experiment File Template

```markdown
# [Experiment Name]
project: [project name]
status: proposed | running | concluded
started: YYYY-MM-DD
hypothesis: [what we're testing]
variant_a: [control - what exists now]
variant_b: [treatment - what we're testing]
metric: [what we measure]
metric_source: [where to check - URL, API, command]
baseline: [current value]
target: [what success looks like]
decision_criteria: [N days of data OR >95% significance]
results:
  - YYYY-MM-DD: [value] ([note])
winner: [declared when concluded]
learning: [what this teaches us]
```
