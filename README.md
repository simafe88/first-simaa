# Install & load packages
packages <- c("plotly")
lapply(packages, function(p) if (!require(p, character.only = TRUE)) install.packages(p))

library(plotly)

# ---- Simulate patient lab data ----
set.seed(2025)
patients <- data.frame(
  PatientID = 1:80,
  BloodPressure = rnorm(80, mean = 120, sd = 15),
  Cholesterol   = rnorm(80, mean = 200, sd = 30),
  Glucose       = rnorm(80, mean = 100, sd = 20)
)

# ---- Run K-means clustering (3 groups) ----
set.seed(123)
km <- kmeans(patients[, -1], centers = 3)
patients$Cluster <- factor(km$cluster)

# ---- 3D Visualization ----
fig <- plot_ly(
  patients, x = ~BloodPressure, y = ~Cholesterol, z = ~Glucose,
  color = ~Cluster, colors = c("red", "blue", "green"),
  type = "scatter3d", mode = "markers", marker = list(size = 5)
)

fig <- fig %>%
  layout(
    title = "3D Patient Clustering (Blood Pressure, Cholesterol, Glucose)",
    scene = list(
      xaxis = list(title = "Blood Pressure"),
      yaxis = list(title = "Cholesterol"),
      zaxis = list(title = "Glucose")
    )
  )

fig
# first-simaa
just testing
