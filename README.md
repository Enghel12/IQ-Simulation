# IQ Simulation Project

## Overview
This project is an R-based simulation designed to explore how different training programs might influence cognitive development, as measured by IQ. It generates baseline IQ scores for 200 participants and assigns them to four distinct groups—from **Intensive + Math** to **None + No Math**. Tailored IQ boosts are then applied to simulate the potential benefits of each training intervention.

## Technical Details
- **Data Generation:**  
  Baseline IQ scores are generated using a normal distribution (mean = 100, SD = 5), representing the initial cognitive performance of each participant.

- **Training Programs:**  
  Participants are split into four groups:
  - **Intensive + Math:** Receives the highest IQ boost.
  - **Moderate + Math:** Receives a moderate IQ boost.
  - **Weak + No Math:** Receives a minimal IQ boost.
  - **None + No Math:** Receives no IQ boost.  
  The IQ boosts are calculated based on the training program's intensity and whether it includes a math component, simulating the impact of cognitive training.

- **Visualization and Analysis:**  
  The project uses `ggplot2` to create box plots that compare IQ scores before and after training. It also employs `dplyr` to compute summary statistics (mean, standard deviation, range, etc.), providing a detailed view of how each training program affects cognitive performance.

## Future Directions
The simulation's box plots and summary statistics suggest that more intensive, math-enhanced training programs lead to significant improvements in IQ scores. Researchers can transform this simulation into a real-world experiment by:
- Creating tailored training programs.
- Involving participants in separate groups.
- Testing whether the mean IQ of each group increases as predicted.
- Determining if the differences between groups are statistically significant.

## Conclusion
This project not only demonstrates potential cognitive enhancements through simulated training programs but also serves as a promising starting point for further research. By validating these simulated improvements in a real-world setting, future studies could establish effective strategies for enhancing cognitive development.
