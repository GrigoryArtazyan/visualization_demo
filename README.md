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
