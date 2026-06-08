# ============================================
# Vocabulary Development Analysis
# Wordbank (MacArthur-Bates CDI) Data
# Emma Higgins | 2026
# ============================================

library(wordbankr)
library(tidyverse)

# Load administration data for English (American) WG form
# WG = Words & Gestures form, administered to children 8-18 months
# WG form explicitly captures both comprehension and production separately
admin_data <- get_administration_data(
  language = "English (American)", 
  form = "WG"
)

# Preview the data
glimpse(admin_data)

# ============================================
# PLOT 1: Vocabulary Growth Trajectories
# How production and comprehension grow with age
# ============================================

# Summarize average comprehension and production by age
growth <- admin_data %>%
  group_by(age) %>%
  summarize(
    mean_comprehension = mean(comprehension, na.rm = TRUE),
    mean_production = mean(production, na.rm = TRUE)
  ) %>%
  pivot_longer(
    cols = c(mean_comprehension, mean_production),
    names_to = "measure",
    values_to = "vocab_size"
  )

# Plot
ggplot(growth, aes(x = age, y = vocab_size, color = measure)) +
  geom_line(size = 1.2) +
  geom_point(size = 2) +
  scale_color_manual(
    values = c("mean_comprehension" = "#2196F3", "mean_production" = "#E91E63"),
    labels = c("Comprehension", "Production")
  ) +
  labs(
    title = "Vocabulary Growth in Early Childhood",
    subtitle = "Average comprehension and production across ages 16–30 months",
    x = "Age (months)",
    y = "Mean Vocabulary Size (words)",
    color = "Measure",
    caption = "Data source: Wordbank (Frank et al., 2017)"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(face = "bold", size = 14),
    legend.position = "bottom"
  )

# ============================================
# PLOT 2: Individual Variation by Age
# How much do children of the same age differ?
# ============================================

# Plot every child's production score as a point, with a smoothed average
ggplot(admin_data, aes(x = age, y = production)) +
  geom_jitter(alpha = 0.2, size = 0.8, color = "#E91E63", width = 0.2) +
  geom_smooth(method = "loess", color = "#880E4F", se = TRUE) +
  labs(
    title = "Individual Variation in Vocabulary Production",
    subtitle = "Each point represents one child — same age, very different outcomes",
    x = "Age (months)",
    y = "Production Vocabulary Size (words)",
    caption = "Data source: Wordbank (Frank et al., 2017)"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(face = "bold", size = 14)
  )

# ============================================
# PLOT 3: The Comprehension-Production Gap
# How much more do children understand than they can say?
# ============================================

# Calculate the gap between comprehension and production for each child
# Filter out rows where comprehension is 0 to avoid division issues
gap_data <- admin_data %>%
  filter(comprehension > 0) %>%
  group_by(age) %>%
  summarize(
    mean_comprehension = mean(comprehension, na.rm = TRUE),
    mean_production = mean(production, na.rm = TRUE),
    gap = mean_comprehension - mean_production,
    ratio = mean_comprehension / mean_production
  )

# Plot the raw gap (comprehension minus production)
ggplot(gap_data, aes(x = age, y = gap)) +
  geom_col(fill = "#2196F3", alpha = 0.7) +
  geom_line(color = "#0D47A1", size = 1.2) +
  labs(
    title = "The Comprehension-Production Gap in Early Language",
    subtitle = "Children understand far more words than they can produce",
    x = "Age (months)",
    y = "Gap (Comprehension minus Production, words)",
    caption = "Data source: Wordbank (Frank et al., 2017)"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(face = "bold", size = 14)
  )

# ============================================
# SAVE PLOTS
# ============================================

# Create a folder for plots
dir.create("plots", showWarnings = FALSE)

# Save Plot 1
growth_plot <- ggplot(growth, aes(x = age, y = vocab_size, color = measure)) +
  geom_line(linewidth = 1.2) +
  geom_point(size = 2) +
  scale_color_manual(
    values = c("mean_comprehension" = "#2196F3", "mean_production" = "#E91E63"),
    labels = c("Comprehension", "Production")
  ) +
  labs(
    title = "Vocabulary Growth in Early Childhood",
    subtitle = "Average comprehension and production across ages 8–18 months",
    x = "Age (months)",
    y = "Mean Vocabulary Size (words)",
    color = "Measure",
    caption = "Data source: Wordbank (Frank et al., 2017)"
  ) +
  theme_minimal() +
  theme(plot.title = element_text(face = "bold", size = 14),
        legend.position = "bottom")

ggsave("plots/plot1_vocab_growth.png", growth_plot, width = 8, height = 5, dpi = 300)

# Save Plot 2
variation_plot <- ggplot(admin_data, aes(x = age, y = production)) +
  geom_jitter(alpha = 0.2, size = 0.8, color = "#E91E63", width = 0.2) +
  geom_smooth(method = "loess", color = "#880E4F", se = TRUE) +
  labs(
    title = "Individual Variation in Vocabulary Production",
    subtitle = "Each point represents one child — same age, very different outcomes",
    x = "Age (months)",
    y = "Production Vocabulary Size (words)",
    caption = "Data source: Wordbank (Frank et al., 2017)"
  ) +
  theme_minimal() +
  theme(plot.title = element_text(face = "bold", size = 14))

ggsave("plots/plot2_individual_variation.png", variation_plot, width = 8, height = 5, dpi = 300)

# Save Plot 3
gap_plot <- ggplot(gap_data, aes(x = age, y = gap)) +
  geom_col(fill = "#2196F3", alpha = 0.7) +
  geom_line(color = "#0D47A1", linewidth = 1.2) +
  labs(
    title = "The Comprehension-Production Gap in Early Language",
    subtitle = "Children understand far more words than they can produce",
    x = "Age (months)",
    y = "Gap (Comprehension minus Production, words)",
    caption = "Data source: Wordbank (Frank et al., 2017)"
  ) +
  theme_minimal() +
  theme(plot.title = element_text(face = "bold", size = 14))

ggsave("plots/plot3_comp_prod_gap.png", gap_plot, width = 8, height = 5, dpi = 300)