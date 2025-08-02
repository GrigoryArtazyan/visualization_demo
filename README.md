## 📊 LEGO Set Pricing Analysis in R

This script uses the [`brickset`](https://cran.r-project.org/web/packages/brickset/index.html) R package to analyze how the **number of pieces** in a LEGO set relates to its **Canadian retail price**. By fitting a linear regression model, we estimate how much each additional LEGO piece contributes to the overall price.

> **Data Source**: [Brickset.com](https://brickset.com) — your comprehensive LEGO set guide (1970–2024 data).

---

### 🔧 Setup

```r
# Install and load the required package
install.packages("brickset")  # if not already installed
library(brickset)

# Load the dataset
data("legosets")

# Inspect column names to find relevant fields
colnames(legosets)
```

---

### 🧹Filtering out rows with missing or zero price/piece values
```r
lego_analysis_data <- subset(legosets, !is.na(CA_retailPrice) & CA_retailPrice > 0 & pieces > 0)
```


---

### 📈 Linear Regression Plot
```r
library(ggplot2)

# Create regression plot
plot <- ggplot(lego_analysis_data, aes(x = pieces, y = CA_retailPrice)) +
  geom_point(alpha = 0.5, color = "#E4002B") +  # LEGO red points
  geom_smooth(method = "lm", se = TRUE, color = "#0055A9", linewidth = 1.5) +  # LEGO blue line
  labs(
    title = "Cost of LEGO Sets by Number of Pieces\nLinear Model: Price ≈ 17.17 + 0.1014×Pieces",
    x = "Number of LEGO Pieces",
    y = "Retail Price in CAD"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(face = "bold", size = 16, hjust = 0.5),
    axis.title = element_text(face = "bold")
  ) +
  xlim(0, 6000) +
  ylim(0, 800)

# Display the plot
print(plot)
```

---

### 📉 Linear Model Summary
```r
# Fit linear regression: price ~ number of pieces
lm_model <- lm(CA_retailPrice ~ pieces, data = lego_analysis_data)

# View coefficients
coef(lm_model)

# Full model summary
summary(lm_model)
```

---
📌 Interpretation
The regression model suggests the following relationship:

- Estimated Price ≈ 17.17 + 0.1014 × Pieces

- The intercept of ~$17.17 CAD suggests a base cost associated with branding, packaging, or licensing.

- Each additional piece adds approximately $0.10 CAD to the price.

This supports the intuitive idea that larger sets tend to be more expensive, although this simple model does not account for other factors like theme, exclusivity, or licensing.
