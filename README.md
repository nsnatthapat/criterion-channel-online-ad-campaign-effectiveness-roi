# Criterion Channel Advertising Experiment Analysis

## Problem
Criterion Channel ran a controlled advertising experiment to evaluate whether ad exposure increased subscriptions and to determine which channels generated positive business value. The core business question is whether paid impressions drove incremental conversions and ROI, and how results should inform channel allocation decisions.

## Key Findings
- The experiment includes 1,200,093 users and 3,924,541 total impressions.
- Treatment materially outperformed control on conversion rate: 1.3409% (95% CI: 1.3163%-1.3655%) vs 0.2992% (95% CI: 0.2813%-0.3170%).
- Absolute lift was +1.04 percentage points (95% CI: +1.01 to +1.07), equivalent to roughly +348% relative lift.
- Randomization quality was weak: average impressions were higher in control (3.58, 95% CI: 3.53-3.63) than treatment (3.14, 95% CI: 3.11-3.16).
- By channel ROI, Twitter was the most reliable positive contributor (ROI = 17.11, 95% bootstrap CI: 16.65-17.47).
- Instagram showed high estimated ROI (35.88, 95% bootstrap CI: 33.18-38.53) but very low volume (5,748 impressions) and a non-significant interaction effect (p = 0.593), indicating an underpowered estimate.
- Facebook, YouTube, and Letterboxd had negative ROI under the modeled incremental impact.

## Dataset
The analysis uses [criterion.csv](criterion.csv), a user-level experiment dataset with:
- Treatment assignment (`treatment`: 1 = treated, 0 = control)
- Outcome (`subscription`: 1 = converted, 0 = not converted)
- Channel-level impression counts (`imp_facebook`, `imp_twitter`, `imp_instagram`, `imp_youtube`, `imp_letterboxd`)
- Derived total exposure (`total_impressions`)

## Methodology
The project evaluates campaign impact in three layers:
- Causal comparison of treatment vs control conversion outcomes.
- Exposure-response analysis by impression frequency bins to assess how lift changes with ad intensity.
- Channel-level incremental value estimation by isolating each channel's ad effect and converting incremental subscriptions into ROI using campaign economics.

Uncertainty is reported throughout using 95% confidence intervals. Rate and lift intervals use standard error-based approximations, while channel-level lift and ROI intervals are estimated with bootstrap resampling on treated-user prediction deltas.

The approach emphasizes decision relevance: identifying where advertising creates measurable incremental value and where spend should be reduced or revalidated.

## Results
Treatment users converted at a substantially higher rate than control users, indicating strong directional evidence that advertising increased subscriptions. However, group imbalance in impressions means the effect size should be interpreted cautiously.

Frequency-level results show positive lift across most practical impression ranges, with particularly strong gains in several mid-range bins and the highest bin. Some extreme bins have sparse control observations, creating unstable estimates and limiting confidence in those segments.

Channel economics indicate a clear allocation signal:
- Scale/defend Twitter as the primary performance channel.
- Re-test Instagram with more volume before scaling aggressively.
- Reduce or redesign spend on Facebook, YouTube, and Letterboxd pending improved creative/targeting or a new test design.

Instagram's positive ROI estimate should not be treated as decision-grade on its own. Its channel interaction term is non-significant (p = 0.593), and its impression base is substantially smaller than the other channels, which is consistent with low statistical power despite a positive point estimate.

## Conclusion
The campaign likely created meaningful incremental conversions, but experimental imbalance weakens strict causal confidence. From a budget standpoint, Twitter is the strongest near-term bet, Instagram is a promising but underpowered opportunity, and other channels should be deprioritized until performance improves.

Key limitation: imperfect randomization and sparse data in some high-exposure bins can bias point estimates.

## Interesting Next Steps and Insights for Future
- Conduct a follow-up experiment with improved randomization and balanced exposure to validate findings.
- More data on customer attributes to test true randomization and identify potential confounders, e.g by geography, device, gender, age, or prior engagement.
- If the marketing team wonders why instagram was not effective and underpowered, a follow-up experiment with more volume and perhaps multiple creative variations could help determine if the channel has potential with better execution or if it is simply not a good fit for the audience.
- Control/Treatment ratio was 70/30. Ratio could be tweaked to either be more balanced for better randomziation, or if management is concerned about opportunity cost of a larger control group, a more aggressive ratio (e.g. 80/20) could be tested to maximize treated volume while still maintaining a reasonable control size for comparison. If management decides to remove control entirely, other methods will have to be explored for counterfactual estimation, but these will have more assumptions and less causal certainty than a randomized control group.

## Repository Structure
- [The_Criterion_Channel.ipynb](The_Criterion_Channel.ipynb): Main analysis notebook.
- [criterion.csv](criterion.csv): Raw experiment data.
- [Case - Criterion Channel.pdf]([Case]%20Criterion%20Channel.pdf): Case brief and business context.
- [README.md](README.md): Portfolio-style project summary.
- outputs/: Generated charts from the visualization code.

## How to Run
1. Open [The_Criterion_Channel.ipynb](The_Criterion_Channel.ipynb).
2. Run the notebook from top to bottom to reproduce metrics.
3. Review this README for the executive summary and business recommendations.
