# Lab 2: Free-Space Path Loss (FSPL) Analysis

**Notebook:** [`lab2-fspl-wireless-path-loss.ipynb`](../labs/lab2-fspl-wireless-path-loss.ipynb)

## Problem Statement
Wireless signal strength weakens as a signal travels farther from its transmitter. Before deploying or troubleshooting a wireless network (e.g., a 2.4 GHz Wi-Fi network), engineers need to predict how much signal power is lost purely due to distance, so that access point placement, coverage radius, and link budgets can be planned correctly. This lab models that relationship for a 2.4 GHz signal (standard Wi-Fi band).

## Methods and Tools
- **Tools:** Python, NumPy, Pandas, Matplotlib
- **Model used:** The Free-Space Path Loss (FSPL) formula:

  `FSPL(dB) = 20·log₁₀(d) + 20·log₁₀(f) + 32.44`

  where `d` is distance in km and `f` is frequency in MHz.
- **Approach:**
  1. Fixed the frequency at 2400 MHz (2.4 GHz Wi-Fi band).
  2. Generated 100 evenly spaced distance values from 0.1 km to 20 km.
  3. Calculated FSPL in dB for each distance.
  4. Cross-checked the calculated values against a reference dataset (`fspl_2400MHz.csv`) loaded into a DataFrame.
  5. Plotted path loss (dB) versus distance (km) to visualize the relationship.

## Results
- Path loss increases logarithmically with distance, for example, loss rose from about **80 dB at 0.1 km** to roughly **94 dB at 0.5 km**, illustrating the sharp early rolloff typical of the inverse-square law underlying FSPL.
- The resulting curve confirmed the expected shape: a steep loss increase at short range that gradually flattens at longer distances, consistent with the logarithmic term in the FSPL equation.

## Interpretation
This lab demonstrated a fundamental telecommunications concept: signal loss is not linear with distance, it is logarithmic. 
