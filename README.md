# Public-Health-Decision-Analysis

This project implements a quantitative decision analysis pipeline to evaluate and compare city-level type 2 diabetes prevention programs under uncertainty in public engagement and behavior change. The project combines expected value modeling, decision trees, and constrained portfolio optimization to support evidence-based program selection.

## Project Overview
The case study models five-year outcomes for a public health department choosing between mass media campaigns and community-based interventions to reduce new type 2 diabetes cases. It then extends to a four-program portfolio with additional gym/nutrition subsidies and a city health app, subject to budget, capacity, synergy, and human resource constraints.

### Problem formulation
- Objective: Maximize expected reduction in new diabetes cases over a five-year horizon.  
- Uncertainty structure:  
  - Stage 1: Public engagement level (low, medium, high) with program-specific prior probabilities.  
  - Stage 2: Behavior change outcome (significant, minor, none) conditional on engagement, with associated probabilities and case reduction impacts.  
- Programs:
  - Mass Media Campaign (2.5B)  
  - Community Intervention Program (1.8B)  
  - Gym & Nutrition Subsidy Program (0.5B)  
  - City Health App (0.3B)

### Expected value modeling
Expected case reductions are computed for each program by:
- Encoding engagement and behavior-change probabilities and impacts in tabular form.  
- Aggregating over all branches:  
$$\text{EV} = \sum_{\text{engagement}} P(e) \sum_{\text{behavior}} P(b \mid e) \times \text{impact}(e,b)$$


Resulting expected reductions:
- Mass Media Campaign: ≈ 462.75 cases  
- Community Intervention Program: ≈ 899.75 cases  

***

## Decision Menu (Two-Program Comparison)

### Decision menu – base programs

| Program                 | Expected Reduction (cases) | Investment Cost (B$) |
|------------------------|---------------------------:|---------------------:|
| Mass Media Campaign    | 462.75                    | 2.5                  |
| Community Intervention | 899.75                    | 1.8                  |

The Community Intervention Program achieves a higher expected reduction at a lower cost, making it the more efficient standalone option compared to the mass media campaign.

***

## Decision Tree Analysis (DADT)
The project builds a decision tree with:
- A top-level decision node for program choice (media vs community).  
- Chance nodes for engagement levels and subsequent behavior-change outcomes on each branch.  
- Terminal nodes representing case reduction payoffs.  

Rollback evaluation recovers the same expected values as the analytical EV calculation and provides a visual explanation of how engagement and behavior uncertainty drive program effectiveness.

***

## Program Portfolio Optimization
In the extended scenario, feasible combinations of up to two programs are evaluated under:
- Budget constraint: Total cost ≤ 5B  
- Capacity constraint: At most two programs run simultaneously  
- Synergy constraint: Gym & Nutrition Subsidies can only be selected if the Mass Media Campaign is also selected  
- HR constraint: Mass Media Campaign and City Health App cannot be run together  

Each feasible combination is scored by summing expected case reductions and total costs.

### Optimal program portfolio

| Selected Programs                      | Expected Reduction (cases) | Total Cost (B$) |
|---------------------------------------|---------------------------:|----------------:|
| Mass Media Campaign + Gym & Nutrition | 1412.75                   | 3.0             |

The optimal portfolio pairs the Mass Media Campaign with the Gym & Nutrition Subsidy Program, delivering the highest expected reduction while staying within the budget and all operational constraints.
