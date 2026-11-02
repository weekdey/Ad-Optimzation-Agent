# Ad Optimization Agent

This project prototypes an advertising budget optimization agent. The agent allocates a fixed daily budget across Search, Social, and Display to maximize expected conversions.

## Project contents

```text
data/cleaned_ad_data.csv
notebooks/Ad_Optimization_Agent.ipynb
results/decision_log.csv
results/evaluation_results.csv
```

## How to run

1. Open `notebooks/Ad_Optimization_Agent.ipynb` in Google Colab.
2. Upload `data/cleaned_ad_data.csv` when the notebook asks for the file.
3. Run the notebook cells from top to bottom.
4. Review the validation checks, budget decisions, decision log, evaluation table, and chart.
5. Download or save `decision_log.csv` and `evaluation_results.csv` in the `results` folder.

The notebook uses Python with pandas, NumPy, and Matplotlib. No advertising platform account or API key is required.

## Agent logic

The agent begins with an equal split of a $1,000 daily budget. After each day, it calculates each channel's conversion efficiency using previous performance data. It shifts budget toward the channel with the highest conversion efficiency and away from the channel with the lowest conversion efficiency.

The agent applies these guardrails:

- Every channel keeps at least 15% of the daily budget.
- A channel's budget cannot change by more than 20% in one day.
- No channel receives a zero-dollar allocation.
- The agent logs the reason for every budget decision.

## Dataset assumptions

The dataset is synthetic and contains 21 days of data for three channels. Each date has one row for Search, Social, and Display. The columns are `date`, `channel`, `spend`, `impressions`, `clicks`, and `conversions`.

The evaluation estimates conversions by applying each day's observed channel conversion efficiency to the proposed budget. The results represent a simulation and do not guarantee real advertising performance.

## Results snapshot

The optimization agent was compared with an equal-split baseline using the same $1,000 daily budget.

| Approach | Expected conversions | Average CPA |
|---|---:|---:|
| Equal split baseline | 2,471.83 | $8.50 |
| Optimization agent | 2,914.96 | $7.20 |

In this simulation, the optimization agent produced more expected conversions and a lower average CPA. The final simulated allocation was approximately $516.67 for Search, $333.33 for Social, and $150.00 for Display. Display remained at the minimum allocation so the agent could continue collecting data from that channel.

## Limitations

The dataset is simulated, and the evaluation uses observed conversion efficiency as an estimate of future performance. A production system would need live advertising data, API authentication, attribution rules, monitoring, and human approval for major budget changes.
