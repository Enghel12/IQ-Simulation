# ==============================================================
# PART 1: SETUP AND DATA STRUCTURES
# ==============================================================

library(ggplot2)
library(dplyr)

# Define the training programs data frame (same as before)
training_programs_df <- data.frame(
  Program = factor(rep(c("Intensive", "Moderate", "Weak", "None"), each = 50)),
  Math_Involved = factor(rep(c("Yes", "No"), each = 100))
)

# For each training-program row, define how much IQ to add
training_programs_df$IqIncrease <- ifelse(training_programs_df$Program == "Intensive", 4, 
                                          ifelse(training_programs_df$Program == "Moderate", 3, 
                                                 ifelse(training_programs_df$Program == "Weak", 2, 0))) +
  ifelse(training_programs_df$Math_Involved == "Yes", 2, 0)

# ==============================================================
# PART 2: RUNNING AND REPLICATING THE EXPERIMENT
# ==============================================================


# Function used to create box plots for group comparison
boxplot_for_group_comparison <- function(before_df, after_df) {
  combined_df <- rbind(before_df, after_df)
  
  # 1. Create the box plot
  
  print(
    ggplot(combined_df, aes(x = ProgramGroup, y = Current_IQ, fill = Current_Group)) + 
      geom_boxplot(position = position_dodge(width = 0.9)) + 
      theme_minimal() +
      labs(
        title = "IQ by Group (Before vs. After)",
        x = "Training Program Group",
        y = "IQ"
      )
  )
  
  # 2. Print a statistical summary for each group x stage
  
  summary_stats <- combined_df %>% 
    group_by(ProgramGroup, Current_Group) %>%
    
    summarize(
      count = n(),
      mean_IQ = mean(Current_IQ),
      sd_IQ = sd(Current_IQ),
      min_IQ = min(Current_IQ),
      max_IQ = max(Current_IQ),
      .groups = "drop"
    )
  
  print(summary_stats)
  
}

running_experiment <- function() {
  # 0. Creating data frames to hold two groups, the group before and after the experiment
  before_group <- data.frame(
    Current_Group = rep("Before", 200), 
    Current_IQ    = rep(0,        200),
    ProgramGroup  = rep("",       200)  # <-- new column to label each participant's group
  )
  after_group <- data.frame(
    Current_Group = rep("After", 200), 
    Current_IQ    = rep(0,       200),
    ProgramGroup  = rep("",      200)
  )
  
  # 1. Create fresh IQ scores for 200 participants
  participants_iq_df <- data.frame(
    Participant = 1:200,
    IQ = rnorm(200, mean = 100, sd = 5)  # new random draws each time
  )
  
  # 2. Label each participant with a subgroup in the "before" data
  #    (1-50 = Intensive+Math, 51-100 = Moderate+Math, etc.)
  before_group$ProgramGroup[1:50]      <- "Intensive + Math"
  before_group$ProgramGroup[51:100]    <- "Moderate + Math"
  before_group$ProgramGroup[101:150]   <- "Weak + No Math"
  before_group$ProgramGroup[151:200]   <- "None + No Math"
  
  # 3. Save the baseline IQ into before_group
  before_group$Current_IQ <- participants_iq_df$IQ  
  
  # ------------------ Splitting & Boosting ------------------ #
  # 4. Split them into four groups of 50
  intensive_and_math_group   <- participants_iq_df[1:50,   ]
  moderate_and_math_group    <- participants_iq_df[51:100,  ]
  weak_and_no_math_group     <- participants_iq_df[101:150, ]
  no_training_no_math_group  <- participants_iq_df[151:200, ]
  
  # 5. Apply the boost
  intensive_and_math_group$IQ <- intensive_and_math_group$IQ + training_programs_df$IqIncrease[1:50]
  moderate_and_math_group$IQ  <- moderate_and_math_group$IQ  + training_programs_df$IqIncrease[51:100]
  weak_and_no_math_group$IQ   <- weak_and_no_math_group$IQ   + training_programs_df$IqIncrease[101:150]
  no_training_no_math_group$IQ<- no_training_no_math_group$IQ + training_programs_df$IqIncrease[151:200]
  
  # 6. Combine into a final "after" data set
  final_df <- rbind(
    intensive_and_math_group,
    moderate_and_math_group,
    weak_and_no_math_group,
    no_training_no_math_group
  )
  
  # 7. Label the subgroups in "after_group" to match the same row order
  after_group$ProgramGroup[1:50]       <- "Intensive + Math"
  after_group$ProgramGroup[51:100]     <- "Moderate + Math"
  after_group$ProgramGroup[101:150]    <- "Weak + No Math"
  after_group$ProgramGroup[151:200]    <- "None + No Math"
  
  # 8. Assign the updated IQ
  after_group$Current_IQ <- final_df$IQ
  
  
  boxplot_for_group_comparison(before_group, after_group)
  
}
running_experiment()







