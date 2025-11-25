# TideStats — Technical Overview of Indices and Scoring Model

TideStats is an analytics framework designed to quantify individual developer contribution through a family of magnitude-based indices. Each index captures a distinct operational dimension of participation in a collaborative software project, using GitHub events as its empirical substrate. The system reduces heterogeneous activity (discussions, reviews, code submissions, PR dynamics) to measurable vectors, making contributions comparable across different developer profiles.

The core principle is straightforward: each contribution dimension is formalized as a vector, and the index is the norm of that vector—representing the consolidated intensity of activity in that axis. This avoids distortions common in raw event counting and creates stable, meaningful indicators.

## Engagement Magnitude Index (REMI)

REMI measures conversational engagement: issue creation, issue comments, PR reviews, and PR comments. These events form the coordinates of a two-dimensional vector (issue interactions; PR interactions). The Euclidean norm expresses overall conversational presence.

**What it measures:** how actively a developer participates in shaping the project through discussion and review.

## Relative Delivery Magnitude Index (RDMI)

RDMI tracks effective code delivery. It combines total code changes (additions + deletions) with the number of closed PRs. These components define a vector whose norm captures the intensity of actual code contribution.

**What it measures:** the developer’s concrete impact on the codebase, including both volume and closure of complete units of work.

## Workload Balance Index (WBI)

WBI measures team-level balance between opened and closed PRs:

$$
WBI = \frac{\text{PRs Closed} - \text{PRs Opened}}{\text{PRs Closed} + \text{PRs Opened}}
$$

Positive values indicate backlog reduction; negative values indicate accumulation.

**What it measures:** the operational climate—whether the team is resolving or accumulating work.

## Execution Balance Index (EBI)

EBI compares the relative weight of discussion-oriented activity (REMI) to delivery-oriented activity (RDMI). It expresses how balanced the team is between planning/coordination and execution.

**What it measures:** whether the cycle leans toward debate, production, or equilibrium.

## The Radar Plot

The radar plot visualizes all indices simultaneously. Each axis corresponds to a normalized index, and each developer forms a polygonal signature:

- wide polygons indicate versatile contributors,
- sharp spikes indicate specialists,
- compact shapes indicate low overall activity.

This offers an immediate profile of strengths and participation patterns.

## The TideStats Score

The score aggregates three components:

1. **activity**, indicating whether REMI and RDMI are strictly positive, weighted by user-defined parameters;
2. **reward**, a weighted average of REMI and RDMI magnitudes;
3. **final score**, computed by interpolation:

$$
\text{score} = s \cdot \text{activity} + (1 - s) \cdot \text{reward}
$$

The score combines minimal participation with actual quantitative contribution, producing a unified metric for cross-developer comparison.

It represents the developer’s consolidated multidimensional contribution, adjustable according to the project’s preferred balance between presence, impact, and consistency.
