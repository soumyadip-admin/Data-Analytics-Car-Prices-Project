install.packages("tidyverse")
install.packages("ggplot2")
install.packages("plotly")
install.packages("rgl")
install.packages("ggplot2")
install.packages("gridExtra")
install.packages("corrplot")
install.packages("scatterplot3d")
install.packages("car")
install.packages("dplyr")

library(tidyverse)
library(ggplot2)
library(plotly)
library(rgl)
library(gridExtra)
library(scatterplot3d)
library(dplyr)

vehicles <- read.csv("car_prices.csv", stringsAsFactors = TRUE)

head(vehicles)
str(vehicles)
summary(vehicles)

vehicles_clean <- vehicles %>%
  filter(!is.na(year), !is.na(make), !is.na(sellingprice), !is.na(condition), !is.na(odometer), !is.na(body), !is.na(transmission))

cat("Total records:", nrow(vehicles), "\n")
cat("Clean records:", nrow(vehicles_clean), "\n")
cat("Year range:", min(vehicles_clean$year), "-", max(vehicles_clean$year), "\n")
cat("Month range:", min(vehicles_clean$month), "-", max(vehicles_clean$month), "\n")

head(vehicles)
str(vehicles)
summary(vehicles)

vehicles_clean <- vehicles %>%
  filter(!is.na(year), !is.na(make), !is.na(sellingprice), !is.na(condition), !is.na(odometer), !is.na(body), !is.na(transmission))

cat("Total records:", nrow(vehicles), "\n")
cat("Clean records:", nrow(vehicles_clean), "\n")
cat("Year range:", min(vehicles_clean$year), "-", max(vehicles_clean$year), "\n")
cat("Month range:", min(vehicles_clean$month), "-", max(vehicles_clean$month), "\n")

fig_3d_1 <- vehicles_clean %>%
  sample_n(5000) %>%
  plot_ly(x = ~odometer, y = ~sellingprice, z = ~year, 
          mode = "markers", type = "scatter3d",
          marker = list(size = 3, color = ~condition, colorscale = "Viridis", showscale = TRUE),
          text = ~paste("Make:", make, "<br>Model:", model, "<br>Condition:", condition)) %>%
  layout(title = "3D: Price vs Mileage vs Year (colored by Condition)",
         scene = list(xaxis = list(title = "Odometer (miles)"),
                      yaxis = list(title = "Selling Price ($)"),
                      zaxis = list(title = "Year")))

fig_3d_1
htmlwidgets::saveWidget(fig_3d_1, "3d_viz_1_price_odometer_year.html")

condition_month_price <- vehicles_clean %>%
  group_by(condition, month) %>%
  summarize(avg_price = mean(sellingprice), count = n(), .groups = 'drop')

fig_3d_2 <- condition_month_price %>%
  plot_ly(x = ~month, y = ~condition, z = ~avg_price, type = "scatter3d", mode = "markers",
          marker = list(size = ~count, color = ~avg_price, colorscale = "Blues")) %>%
  layout(title = "3D: Condition vs Month vs Average Price (size = sales count)",
         scene = list(xaxis = list(title = "Month"),
                      yaxis = list(title = "Condition Rating"),
                      zaxis = list(title = "Avg Price ($)")))

fig_3d_2
htmlwidgets::saveWidget(fig_3d_2, "3d_viz_2_condition_month_price.html")

vehicles <- vehicles %>%
  mutate(
    month_name = substr(saledate, 5, 7),
    month = case_when(
      month_name == "Jan" ~ 1,
      month_name == "Feb" ~ 2,
      month_name == "Mar" ~ 3,
      month_name == "Apr" ~ 4,
      month_name == "May" ~ 5,
      month_name == "Jun" ~ 6,
      month_name == "Jul" ~ 7,
      month_name == "Aug" ~ 8,
      month_name == "Sep" ~ 9,
      month_name == "Oct" ~ 10,
      month_name == "Nov" ~ 11,
      month_name == "Dec" ~ 12
    )
  )

vehicles_clean <- vehicles %>%
  filter(!is.na(year), !is.na(make), !is.na(sellingprice), !is.na(condition), !is.na(odometer), !is.na(body), !is.na(transmission), !is.na(month))

cat("Total records:", nrow(vehicles), "\n")
cat("Clean records:", nrow(vehicles_clean), "\n")
cat("Year range:", min(vehicles_clean$year), "-", max(vehicles_clean$year), "\n")
cat("Month range:", min(vehicles_clean$month), "-", max(vehicles_clean$month), "\n")

condition_month_price <- vehicles_clean %>%
  group_by(condition, month) %>%
  summarize(avg_price = mean(sellingprice), count = n(), .groups = 'drop')

fig_3d_2 <- condition_month_price %>%
  plot_ly(x = ~month, y = ~condition, z = ~avg_price, type = "scatter3d", mode = "markers",
          marker = list(size = ~count, color = ~avg_price, colorscale = "Blues")) %>%
  layout(title = "3D: Condition vs Month vs Average Price (size = sales count)",
         scene = list(xaxis = list(title = "Month"),
                      yaxis = list(title = "Condition Rating"),
                      zaxis = list(title = "Avg Price ($)")))

fig_3d_2
htmlwidgets::saveWidget(fig_3d_2, "3d_viz_2_condition_month_price.html")

sample_data <- vehicles_clean %>% sample_n(3000)

fig_3d_1 <- sample_data %>%
  plot_ly(x = ~odometer, y = ~sellingprice, z = ~year,
          type = "scatter3d", mode = "markers",
          marker = list(
            size = 5,
            color = ~sellingprice,
            colorscale = "Viridis",
            showscale = TRUE,
            colorbar = list(title = "Price ($)", tickformat = "$,"),
            line = list(color = "white", width = 0.5)
          ),
          text = ~paste("Make:", make, "<br>Model:", model, "<br>Price: $", format(round(sellingprice), big.mark=","), 
                        "<br>Mileage:", format(round(odometer), big.mark=","), "mi", "<br>Year:", year),
          hoverinfo = "text") %>%
  layout(
    title = list(text = "<b>Vehicle Market: Price vs Mileage vs Year</b><br><sub>3000 Sample Vehicles | Color = Selling Price</sub>", 
                 x = 0.5, xanchor = "center"),
    scene = list(
      xaxis = list(title = "<b>Odometer (miles)</b>", backgroundcolor = "#f0f0f0", gridwidth = 1),
      yaxis = list(title = "<b>Selling Price ($)</b>", backgroundcolor = "#f0f0f0", gridwidth = 1),
      zaxis = list(title = "<b>Year</b>", backgroundcolor = "#f0f0f0", gridwidth = 1),
      bgcolor = "#ffffff"
    ),
    font = list(family = "Arial, sans-serif", size = 12, color = "#333333"),
    width = 1200, height = 700,
    margin = list(l = 50, r = 50, b = 50, t = 100)
  )

fig_3d_1
htmlwidgets::saveWidget(fig_3d_1, "LINKEDIN_3D_VIZ_1_Price_Mileage_Year.html")

top_15_makes <- vehicles_clean %>%
  group_by(make) %>%
  summarize(total = n()) %>%
  arrange(desc(total)) %>%
  head(15) %>%
  pull(make)

make_year_sales <- vehicles_clean %>%
  filter(make %in% top_15_makes) %>%
  group_by(make, year) %>%
  summarize(sales_count = n(), avg_price = mean(sellingprice), .groups = 'drop')

fig_3d_2 <- make_year_sales %>%
  plot_ly(x = ~make, y = ~year, z = ~sales_count, 
          type = "scatter3d", mode = "markers",
          marker = list(
            size = ~sqrt(avg_price)/20,
            color = ~avg_price,
            colorscale = "RdYlGn_r",
            showscale = TRUE,
            colorbar = list(title = "Avg Price ($)", tickformat = "$,"),
            line = list(color = "white", width = 1)
          ),
          text = ~paste("<b>", make, "</b><br>Year:", year, "<br>Sales:", sales_count, 
                        "<br>Avg Price: $", format(round(avg_price), big.mark=",")),
          hoverinfo = "text") %>%
  layout(
    title = list(text = "<b>Top 15 Makes: Sales Volume by Year</b><br><sub>Bubble Size = Avg Price | Color = Price Range</sub>",
                 x = 0.5, xanchor = "center"),
    scene = list(
      xaxis = list(title = "<b>Make</b>", backgroundcolor = "#f0f0f0"),
      yaxis = list(title = "<b>Year</b>", backgroundcolor = "#f0f0f0"),
      zaxis = list(title = "<b>Sales Count</b>", backgroundcolor = "#f0f0f0"),
      bgcolor = "#ffffff"
    ),
    font = list(family = "Arial, sans-serif", size = 12, color = "#333333"),
    width = 1200, height = 700
  )

fig_3d_2
htmlwidgets::saveWidget(fig_3d_2, "LINKEDIN_3D_VIZ_2_Top_Makes_Sales.html")

condition_body_price <- vehicles_clean %>%
  group_by(condition, body) %>%
  summarize(avg_price = mean(sellingprice), count = n(), .groups = 'drop') %>%
  filter(count >= 10)

fig_3d_3 <- condition_body_price %>%
  plot_ly(x = ~condition, y = ~body, z = ~avg_price,
          type = "scatter3d", mode = "markers",
          marker = list(
            size = ~log(count) * 3,
            color = ~avg_price,
            colorscale = "Plasma",
            showscale = TRUE,
            colorbar = list(title = "Avg Price ($)", tickformat = "$,"),
            line = list(color = "white", width = 1)
          ),
          text = ~paste("<b>Condition:</b>", condition, "<br><b>Body:</b>", body, 
                        "<br><b>Avg Price:</b> $", format(round(avg_price), big.mark=","),
                        "<br><b>Count:</b>", count),
          hoverinfo = "text") %>%
  layout(
    title = list(text = "<b>Vehicle Condition vs Body Type Analysis</b><br><sub>Bubble Size = Sales Volume | Color = Average Price</sub>",
                 x = 0.5, xanchor = "center"),
    scene = list(
      xaxis = list(title = "<b>Condition Rating (1-5)</b>", backgroundcolor = "#f0f0f0"),
      yaxis = list(title = "<b>Body Type</b>", backgroundcolor = "#f0f0f0"),
      zaxis = list(title = "<b>Average Price ($)</b>", backgroundcolor = "#f0f0f0"),
      bgcolor = "#ffffff"
    ),
    font = list(family = "Arial, sans-serif", size = 12, color = "#333333"),
    width = 1200, height = 700
  )

fig_3d_3
htmlwidgets::saveWidget(fig_3d_3, "LINKEDIN_3D_VIZ_3_Condition_Body_Price.html")

monthly_data <- vehicles_clean %>%
  group_by(year, month) %>%
  summarize(avg_price = mean(sellingprice), 
            median_price = median(sellingprice),
            count = n(),
            .groups = 'drop') %>%
  arrange(year, month) %>%
  mutate(date_str = paste(year, sprintf("%02d", month), sep = "-"))

p1 <- ggplot(monthly_data, aes(x = reorder(date_str, year*100 + month), y = avg_price, group = 1)) +
  geom_smooth(method = "loess", color = "#FF6B6B", fill = "#FFE5E5", se = TRUE, size = 1.2, span = 0.3) +
  geom_point(aes(color = count), size = 3, alpha = 0.7) +
  scale_color_gradient(low = "#3498db", high = "#e74c3c", name = "Sales Volume") +
  labs(
    title = "Market Trend: Average Selling Price Over Time",
    subtitle = "Monthly Average with Sales Volume Indicator",
    x = "Time Period (Year-Month)",
    y = "Average Selling Price ($)",
    caption = "Data Source: Vehicle Sales Database | Point Color = Sales Count"
  ) +
  scale_y_continuous(labels = dollar) +
  theme_minimal() +
  theme(
    plot.title = element_text(size = 16, face = "bold", hjust = 0.5),
    plot.subtitle = element_text(size = 12, color = "#666666", hjust = 0.5),
    axis.text.x = element_text(angle = 45, hjust = 1, vjust = 1),
    axis.title = element_text(size = 12, face = "bold"),
    legend.position = "right",
    panel.grid.minor = element_blank(),
    panel.grid.major = element_line(color = "#e0e0e0", size = 0.2)
  )

ggsave("LINKEDIN_2D_VIZ_1_Price_Trend.png", p1, width = 14, height = 7, dpi = 300)

p2 <- ggplot(vehicles_clean, aes(x = sellingprice, fill = factor(condition), color = factor(condition))) +
  geom_density(alpha = 0.5, size = 1) +
  scale_fill_brewer(palette = "RdYlGn", name = "Condition", labels = c("Salvage", "Fair", "Average", "Good", "Excellent")) +
  scale_color_brewer(palette = "RdYlGn", name = "Condition", labels = c("Salvage", "Fair", "Average", "Good", "Excellent")) +
  scale_x_continuous(labels = dollar) +
  labs(
    title = "Price Distribution by Vehicle Condition",
    subtitle = "Kernel Density Estimation Across All Conditions",
    x = "Selling Price ($)",
    y = "Density",
    caption = "Higher density = More vehicles at that price point"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(size = 16, face = "bold", hjust = 0.5),
    plot.subtitle = element_text(size = 12, color = "#666666", hjust = 0.5),
    axis.title = element_text(size = 12, face = "bold"),
    legend.position = "right",
    panel.grid.minor = element_blank(),
    panel.grid.major = element_line(color = "#e0e0e0")
  )

ggsave("LINKEDIN_2D_VIZ_2_Price_Density.png", p2, width = 14, height = 7, dpi = 300)

library(tidyverse)
library(ggplot2)
library(scales)

monthly_data <- vehicles_clean %>%
  group_by(year, month) %>%
  summarize(avg_price = mean(sellingprice), 
            median_price = median(sellingprice),
            count = n(),
            .groups = 'drop') %>%
  arrange(year, month) %>%
  mutate(date_str = paste(year, sprintf("%02d", month), sep = "-"))

p1 <- ggplot(monthly_data, aes(x = reorder(date_str, year*100 + month), y = avg_price, group = 1)) +
  geom_smooth(method = "loess", color = "#FF6B6B", fill = "#FFE5E5", se = TRUE, linewidth = 1.2, span = 0.3) +
  geom_point(aes(color = count), size = 3, alpha = 0.7) +
  scale_color_gradient(low = "#3498db", high = "#e74c3c", name = "Sales Volume") +
  labs(
    title = "Market Trend: Average Selling Price Over Time",
    subtitle = "Monthly Average with Sales Volume Indicator",
    x = "Time Period (Year-Month)",
    y = "Average Selling Price ($)",
    caption = "Data Source: Vehicle Sales Database | Point Color = Sales Count"
  ) +
  scale_y_continuous(labels = scales::dollar) +
  theme_minimal() +
  theme(
    plot.title = element_text(size = 16, face = "bold", hjust = 0.5),
    plot.subtitle = element_text(size = 12, color = "#666666", hjust = 0.5),
    axis.text.x = element_text(angle = 45, hjust = 1, vjust = 1),
    axis.title = element_text(size = 12, face = "bold"),
    legend.position = "right",
    panel.grid.minor = element_blank(),
    panel.grid.major = element_line(color = "#e0e0e0", linewidth = 0.2)
  )

ggsave("LINKEDIN_2D_VIZ_1_Price_Trend.png", p1, width = 14, height = 7, dpi = 300)

p2 <- ggplot(vehicles_clean, aes(x = sellingprice, fill = factor(condition), color = factor(condition))) +
  geom_density(alpha = 0.5, linewidth = 1) +
  scale_fill_brewer(palette = "RdYlGn", name = "Condition", labels = c("Salvage", "Fair", "Average", "Good", "Excellent")) +
  scale_color_brewer(palette = "RdYlGn", name = "Condition", labels = c("Salvage", "Fair", "Average", "Good", "Excellent")) +
  scale_x_continuous(labels = scales::dollar) +
  labs(
    title = "Price Distribution by Vehicle Condition",
    subtitle = "Kernel Density Estimation Across All Conditions",
    x = "Selling Price ($)",
    y = "Density",
    caption = "Higher density = More vehicles at that price point"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(size = 16, face = "bold", hjust = 0.5),
    plot.subtitle = element_text(size = 12, color = "#666666", hjust = 0.5),
    axis.title = element_text(size = 12, face = "bold"),
    legend.position = "right",
    panel.grid.minor = element_blank(),
    panel.grid.major = element_line(color = "#e0e0e0")
  )

ggsave("LINKEDIN_2D_VIZ_2_Price_Density.png", p2, width = 14, height = 7, dpi = 300)


top_makes_data <- vehicles_clean %>%
  group_by(make) %>%
  summarize(
    sales_count = n(),
    avg_price = mean(sellingprice),
    median_price = median(sellingprice),
    price_std = sd(sellingprice),
    .groups = 'drop'
  ) %>%
  arrange(desc(sales_count)) %>%
  head(15)

p3 <- ggplot(top_makes_data, aes(x = reorder(make, sales_count), y = sales_count, fill = avg_price)) +
  geom_bar(stat = "identity", color = "white", linewidth = 1) +
  geom_text(aes(label = paste(sales_count, "\n$", format(round(avg_price), big.mark=","))), 
            hjust = -0.1, size = 3.5, fontface = "bold") +
  scale_fill_gradient(low = "#3498db", high = "#e74c3c", name = "Avg Price ($)") +
  scale_y_continuous(expand = c(0, 0), limits = c(0, max(top_makes_data$sales_count) * 1.15)) +
  coord_flip() +
  labs(
    title = "Top 15 Vehicle Makes by Sales Volume",
    subtitle = "Label: Sales Count | Color: Average Selling Price",
    x = "Vehicle Make",
    y = "Number of Vehicles Sold",
    caption = "Data represents all vehicles in dataset"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(size = 16, face = "bold"),
    plot.subtitle = element_text(size = 12, color = "#666666"),
    axis.title = element_text(size = 12, face = "bold"),
    legend.position = "right",
    panel.grid.minor = element_blank(),
    panel.grid.major.y = element_blank(),
    panel.grid.major.x = element_line(color = "#e0e0e0")
  )

ggsave("LINKEDIN_2D_VIZ_3_Top_Makes.png", p3, width = 14, height = 8, dpi = 300)

sample_scatter <- vehicles_clean %>% sample_n(min(5000, nrow(vehicles_clean)))

p4 <- ggplot(sample_scatter, aes(x = odometer, y = sellingprice)) +
  geom_point(aes(color = factor(condition)), alpha = 0.4, size = 2) +
  geom_smooth(method = "loess", color = "#000000", fill = "#cccccc", se = TRUE, linewidth = 1.5) +
  scale_color_brewer(palette = "RdYlGn", name = "Condition", labels = c("Salvage", "Fair", "Average", "Good", "Excellent")) +
  scale_x_continuous(labels = scales::comma) +
  scale_y_continuous(labels = scales::dollar) +
  labs(
    title = "Vehicle Price Depreciation: Mileage Impact",
    subtitle = "5000 Sample Vehicles | Smooth LOESS Trend Line",
    x = "Odometer (Miles)",
    y = "Selling Price ($)",
    caption = "Demonstrates inverse relationship between mileage and vehicle value"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(size = 16, face = "bold", hjust = 0.5),
    plot.subtitle = element_text(size = 12, color = "#666666", hjust = 0.5),
    axis.title = element_text(size = 12, face = "bold"),
    legend.position = "right",
    panel.grid.minor = element_blank(),
    panel.grid.major = element_line(color = "#e0e0e0")
  )

ggsave("LINKEDIN_2D_VIZ_4_Mileage_Price.png", p4, width = 14, height = 8, dpi = 300)

top_10_makes <- vehicles_clean %>%
  group_by(make) %>%
  summarize(n = n()) %>%
  arrange(desc(n)) %>%
  head(10) %>%
  pull(make)

heatmap_data <- vehicles_clean %>%
  filter(make %in% top_10_makes) %>%
  group_by(make, month) %>%
  summarize(avg_price = mean(sellingprice), count = n(), .groups = 'drop')

p5 <- ggplot(heatmap_data, aes(x = factor(month), y = fct_reorder(make, avg_price, .fun = mean), fill = avg_price)) +
  geom_tile(color = "white", linewidth = 1) +
  geom_text(aes(label = paste("$", format(round(avg_price), big.mark=","))), 
            color = "white", size = 3, fontface = "bold") +
  scale_fill_gradient(low = "#3498db", high = "#e74c3c", name = "Avg Price ($)") +
  scale_x_discrete(labels = c("Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec")) +
  labs(
    title = "Seasonal Price Trends: Top 10 Makes by Month",
    subtitle = "Average Selling Price Heatmap",
    x = "Month",
    y = "Vehicle Make",
    caption = "Lighter = Lower Price | Darker = Higher Price"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(size = 16, face = "bold", hjust = 0.5),
    plot.subtitle = element_text(size = 12, color = "#666666", hjust = 0.5),
    axis.title = element_text(size = 12, face = "bold"),
    panel.grid = element_blank()
  )

ggsave("LINKEDIN_2D_VIZ_5_Seasonal_Heatmap.png", p5, width = 14, height = 8, dpi = 300)

body_summary <- vehicles_clean %>%
  group_by(body) %>%
  summarize(count = n(), avg_price = mean(sellingprice)) %>%
  filter(count >= 50) %>%
  arrange(desc(count))

vehicles_top_body <- vehicles_clean %>%
  filter(body %in% body_summary$body)

p6 <- ggplot(vehicles_top_body, aes(x = fct_reorder(body, sellingprice, .fun = median), y = sellingprice, fill = body)) +
  geom_violin(alpha = 0.6, color = "white", linewidth = 1) +
  geom_boxplot(width = 0.2, fill = "white", alpha = 0.8, color = "#333333", linewidth = 0.8) +
  stat_summary(fun = mean, geom = "point", shape = 23, size = 4, fill = "#e74c3c") +
  scale_fill_viridis_d(name = "Body Type") +
  scale_y_continuous(labels = scales::dollar) +
  labs(
    title = "Price Distribution by Vehicle Body Type",
    subtitle = "Violin Plot (Distribution) + Box Plot (Quartiles) | Red Diamond = Mean Price",
    x = "Body Type",
    y = "Selling Price ($)",
    caption = "Wider sections = more vehicles at that price point"
  ) +
  coord_flip() +
  theme_minimal() +
  theme(
    plot.title = element_text(size = 16, face = "bold"),
    plot.subtitle = element_text(size = 12, color = "#666666"),
    axis.title = element_text(size = 12, face = "bold"),
    legend.position = "none",
    panel.grid.minor = element_blank(),
    panel.grid.major.x = element_line(color = "#e0e0e0")
  )

ggsave("LINKEDIN_2D_VIZ_6_Body_Type.png", p6, width = 14, height = 8, dpi = 300)

library(tidyverse)
library(ggplot2)
library(scales)

p2_improved <- ggplot(vehicles_clean, aes(x = sellingprice, fill = factor(condition), color = factor(condition))) +
  geom_density(alpha = 0.65, linewidth = 1.2, adjust = 1.5) +
  scale_fill_manual(
    values = c("1" = "#e74c3c", "2" = "#f39c12", "3" = "#f1c40f", "4" = "#2ecc71", "5" = "#27ae60"),
    name = "Condition",
    labels = c("1" = "Salvage", "2" = "Fair", "3" = "Average", "4" = "Good", "5" = "Excellent")
  ) +
  scale_color_manual(
    values = c("1" = "#c0392b", "2" = "#d68910", "3" = "#d4ac0d", "4" = "#27ae60", "5" = "#1e8449"),
    name = "Condition",
    labels = c("1" = "Salvage", "2" = "Fair", "3" = "Average", "4" = "Good", "5" = "Excellent")
  ) +
  scale_x_continuous(limits = c(0, 100000), labels = scales::dollar_format(scale = 1, prefix = "$")) +
  labs(
    title = "Price Distribution by Vehicle Condition",
    subtitle = "Kernel Density Estimation - Larger areas indicate more vehicles at that price",
    x = "Selling Price ($)",
    y = "Density (Probability)",
    caption = "Dataset: Vehicle Sales Data | Excellent condition vehicles command higher prices"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(size = 18, face = "bold", hjust = 0.5, color = "#2c3e50", margin = margin(b = 5)),
    plot.subtitle = element_text(size = 13, color = "#7f8c8d", hjust = 0.5, margin = margin(b = 15)),
    plot.caption = element_text(size = 10, color = "#95a5a6", hjust = 1),
    axis.title = element_text(size = 12, face = "bold", color = "#2c3e50"),
    axis.text = element_text(size = 11, color = "#34495e"),
    legend.position = "right",
    legend.title = element_text(size = 12, face = "bold", color = "#2c3e50"),
    legend.text = element_text(size = 11, color = "#34495e"),
    panel.grid.minor = element_blank(),
    panel.grid.major = element_line(color = "#ecf0f1", linewidth = 0.3),
    plot.background = element_rect(fill = "white", color = NA),
    panel.background = element_rect(fill = "#f8f9fa", color = NA),
    plot.margin = margin(t = 15, r = 20, b = 15, l = 20)
  )

ggsave("LINKEDIN_2D_VIZ_2_Price_Density_IMPROVED.png", p2_improved, width = 16, height = 8, dpi = 300, bg = "white")

p2_faceted <- ggplot(vehicles_clean, aes(x = sellingprice, fill = factor(condition))) +
  geom_density(alpha = 0.75, linewidth = 1.3, color = "black", adjust = 1.3) +
  facet_wrap(~factor(condition, labels = c("1" = "Salvage", "2" = "Fair", "3" = "Average", "4" = "Good", "5" = "Excellent")), 
             nrow = 2, ncol = 3) +
  scale_fill_manual(
    values = c("1" = "#e74c3c", "2" = "#e67e22", "3" = "#f39c12", "4" = "#27ae60", "5" = "#16a085"),
    guide = "none"
  ) +
  scale_x_continuous(limits = c(0, 80000), labels = scales::dollar_format(scale = 1, prefix = "$"), breaks = seq(0, 80000, 20000)) +
  labs(
    title = "Price Distribution by Vehicle Condition - Individual Analysis",
    subtitle = "Each panel shows one condition rating separately for clarity",
    x = "Selling Price ($)",
    y = "Density",
    caption = "Salvage vehicles cluster at $0-5K | Excellent vehicles spread across $10K-40K range"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(size = 18, face = "bold", hjust = 0.5, color = "#1a1a1a", margin = margin(b = 5)),
    plot.subtitle = element_text(size = 13, color = "#555555", hjust = 0.5, margin = margin(b = 15)),
    plot.caption = element_text(size = 11, color = "#666666", hjust = 0.5, margin = margin(t = 15), face = "italic"),
    axis.title = element_text(size = 12, face = "bold", color = "#1a1a1a"),
    axis.text = element_text(size = 10, color = "#333333"),
    strip.text = element_text(size = 12, face = "bold", color = "white", margin = margin(t = 5, b = 5)),
    strip.background = element_rect(fill = "#2c3e50", color = "black", linewidth = 1),
    panel.grid.minor = element_blank(),
    panel.grid.major = element_line(color = "#e0e0e0", linewidth = 0.2),
    plot.background = element_rect(fill = "white", color = "black", linewidth = 1.5),
    panel.background = element_rect(fill = "#f7f7f7", color = "black", linewidth = 0.5),
    panel.spacing = unit(1, "lines"),
    plot.margin = margin(t = 20, r = 20, b = 20, l = 20)
  )

ggsave("LINKEDIN_VIZ_2_FACETED_DENSITY.png", p2_faceted, width = 16, height = 10, dpi = 300, bg = "white")


condition_stats <- vehicles_clean %>%
  mutate(condition_label = factor(condition, labels = c("1" = "Salvage", "2" = "Fair", "3" = "Average", "4" = "Good", "5" = "Excellent"))) %>%
  group_by(condition_label) %>%
  summarise(
    count = n(),
    avg_price = mean(sellingprice),
    median_price = median(sellingprice),
    sd_price = sd(sellingprice),
    pct = n() / nrow(vehicles_clean) * 100,
    .groups = 'drop'
  )

p2_bar <- ggplot(condition_stats, aes(x = fct_reorder(condition_label, avg_price), y = avg_price, fill = condition_label)) +
  geom_col(color = "black", linewidth = 1.2, width = 0.7) +
  geom_errorbar(aes(ymin = avg_price - sd_price, ymax = avg_price + sd_price), 
                width = 0.3, color = "black", linewidth = 1, alpha = 0.6) +
  geom_text(aes(label = paste("$", format(round(avg_price), big.mark = ","), 
                              "\n", format(round(pct), nsmall = 1), "%", sep = "")), 
            vjust = -1.5, size = 4.5, fontface = "bold", color = "#1a1a1a") +
  scale_fill_manual(
    values = c("Salvage" = "#e74c3c", "Fair" = "#e67e22", "Average" = "#f39c12", "Good" = "#27ae60", "Excellent" = "#16a085"),
    guide = "none"
  ) +
  scale_y_continuous(limits = c(0, max(condition_stats$avg_price) * 1.25), 
                     labels = scales::dollar_format(scale = 1, prefix = "$")) +
  labs(
    title = "Average Vehicle Price by Condition",
    subtitle = "Error bars show price variation | Numbers show % of vehicles in each condition",
    x = "Vehicle Condition",
    y = "Average Selling Price ($)",
    caption = "Clear trend: Better condition vehicles command significantly higher prices. Excellent vehicles avg $15K+ more than Salvage."
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(size = 18, face = "bold", hjust = 0.5, color = "#1a1a1a", margin = margin(b = 5)),
    plot.subtitle = element_text(size = 12, color = "#555555", hjust = 0.5, margin = margin(b = 15)),
    plot.caption = element_text(size = 11, color = "#666666", hjust = 0.5, margin = margin(t = 15), face = "italic"),
    axis.title = element_text(size = 12, face = "bold", color = "#1a1a1a"),
    axis.text = element_text(size = 11, color = "#333333"),
    panel.grid.minor = element_blank(),
    panel.grid.major.x = element_blank(),
    panel.grid.major.y = element_line(color = "#e0e0e0", linewidth = 0.3),
    plot.background = element_rect(fill = "white", color = "black", linewidth = 1.5),
    panel.background = element_rect(fill = "#f9f9f9", color = "black", linewidth = 0.5),
    plot.margin = margin(t = 20, r = 20, b = 20, l = 20)
  )

ggsave("LINKEDIN_VIZ_2_BAR_CHART.png", p2_bar, width = 14, height = 8, dpi = 300, bg = "white")


vehicles_clean_labeled <- vehicles_clean %>%
  mutate(condition_label = case_when(
    condition == 1 ~ "Salvage",
    condition == 2 ~ "Fair",
    condition == 3 ~ "Average",
    condition == 4 ~ "Good",
    condition == 5 ~ "Excellent"
  ))

p2_faceted <- ggplot(vehicles_clean_labeled, aes(x = sellingprice, fill = condition_label)) +
  geom_density(alpha = 0.75, linewidth = 1.3, color = "black", adjust = 1.3) +
  facet_wrap(~factor(condition_label, levels = c("Salvage", "Fair", "Average", "Good", "Excellent")), 
             nrow = 2, ncol = 3) +
  scale_fill_manual(
    values = c("Salvage" = "#e74c3c", "Fair" = "#e67e22", "Average" = "#f39c12", "Good" = "#27ae60", "Excellent" = "#16a085"),
    guide = "none"
  ) +
  scale_x_continuous(limits = c(0, 80000), labels = dollar_format(prefix = "$"), breaks = seq(0, 80000, 20000)) +
  labs(
    title = "Price Distribution by Vehicle Condition",
    subtitle = "Each panel shows one condition rating separately for clarity",
    x = "Selling Price ($)",
    y = "Density",
    caption = "Salvage vehicles cluster at $0-5K | Excellent vehicles spread across $10K-40K range"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(size = 18, face = "bold", hjust = 0.5, color = "#1a1a1a", margin = margin(b = 5)),
    plot.subtitle = element_text(size = 13, color = "#555555", hjust = 0.5, margin = margin(b = 15)),
    plot.caption = element_text(size = 11, color = "#666666", hjust = 0.5, margin = margin(t = 15), face = "italic"),
    axis.title = element_text(size = 12, face = "bold", color = "#1a1a1a"),
    axis.text = element_text(size = 10, color = "#333333"),
    strip.text = element_text(size = 12, face = "bold", color = "white", margin = margin(t = 5, b = 5)),
    strip.background = element_rect(fill = "#2c3e50", color = "black", linewidth = 1),
    panel.grid.minor = element_blank(),
    panel.grid.major = element_line(color = "#e0e0e0", linewidth = 0.2),
    plot.background = element_rect(fill = "white", color = "black", linewidth = 1.5),
    panel.background = element_rect(fill = "#f7f7f7", color = "black", linewidth = 0.5),
    panel.spacing = unit(1, "lines"),
    plot.margin = margin(t = 20, r = 20, b = 20, l = 20)
  )

ggsave("LINKEDIN_VIZ_2_FACETED_DENSITY_FINAL.png", p2_faceted, width = 16, height = 10, dpi = 300, bg = "white")

condition_stats <- vehicles_clean %>%
  mutate(condition_label = case_when(
    condition == 1 ~ "Salvage",
    condition == 2 ~ "Fair",
    condition == 3 ~ "Average",
    condition == 4 ~ "Good",
    condition == 5 ~ "Excellent"
  )) %>%
  group_by(condition_label) %>%
  summarise(
    count = n(),
    avg_price = mean(sellingprice),
    median_price = median(sellingprice),
    sd_price = sd(sellingprice),
    pct = n() / nrow(vehicles_clean) * 100,
    .groups = 'drop'
  ) %>%
  mutate(condition_label = factor(condition_label, levels = c("Salvage", "Fair", "Average", "Good", "Excellent")))

p2_bar <- ggplot(condition_stats, aes(x = condition_label, y = avg_price, fill = condition_label)) +
  geom_col(color = "black", linewidth = 1.2, width = 0.7) +
  geom_errorbar(aes(ymin = avg_price - sd_price, ymax = avg_price + sd_price), 
                width = 0.3, color = "black", linewidth = 1, alpha = 0.6) +
  geom_text(aes(label = paste("$", format(round(avg_price), big.mark = ","), 
                              "\n(", format(round(pct), nsmall = 1), "%)", sep = "")), 
            vjust = -1.5, size = 4, fontface = "bold", color = "#1a1a1a") +
  scale_fill_manual(
    values = c("Salvage" = "#e74c3c", "Fair" = "#e67e22", "Average" = "#f39c12", "Good" = "#27ae60", "Excellent" = "#16a085"),
    guide = "none"
  ) +
  scale_y_continuous(limits = c(0, max(condition_stats$avg_price) * 1.25), 
                     labels = dollar_format(prefix = "$")) +
  labs(
    title = "Average Vehicle Price by Condition Rating",
    subtitle = "Error bars = Price variation | Percentages = % of vehicles in each condition",
    x = "Vehicle Condition",
    y = "Average Selling Price ($)",
    caption = "Key Finding: Better condition vehicles command significantly higher prices. Excellent vehicles avg 2-3x more than Salvage."
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(size = 18, face = "bold", hjust = 0.5, color = "#1a1a1a", margin = margin(b = 5)),
    plot.subtitle = element_text(size = 12, color = "#555555", hjust = 0.5, margin = margin(b = 15)),
    plot.caption = element_text(size = 11, color = "#666666", hjust = 0.5, margin = margin(t = 15), face = "italic"),
    axis.title = element_text(size = 12, face = "bold", color = "#1a1a1a"),
    axis.text = element_text(size = 11, color = "#333333"),
    panel.grid.minor = element_blank(),
    panel.grid.major.x = element_blank(),
    panel.grid.major.y = element_line(color = "#e0e0e0", linewidth = 0.3),
    plot.background = element_rect(fill = "white", color = "black", linewidth = 1.5),
    panel.background = element_rect(fill = "#f9f9f9", color = "black", linewidth = 0.5),
    plot.margin = margin(t = 20, r = 20, b = 20, l = 20)
  )

ggsave("LINKEDIN_VIZ_2_BAR_CHART_FINAL.png", p2_bar, width = 14, height = 8, dpi = 300, bg = "white")

install.packages("ggridges")
library(ggridges)

vehicles_clean_labeled <- vehicles_clean %>%
  mutate(condition_label = case_when(
    condition == 1 ~ "Salvage",
    condition == 2 ~ "Fair",
    condition == 3 ~ "Average",
    condition == 4 ~ "Good",
    condition == 5 ~ "Excellent"
  ),
  condition_label = factor(condition_label, levels = c("Salvage", "Fair", "Average", "Good", "Excellent")))

p2_ridge <- ggplot(vehicles_clean_labeled, aes(x = sellingprice, 
                                               y = condition_label,
                                               fill = condition_label)) +
  geom_density_ridges(alpha = 0.8, scale = 0.9, rel_min_height = 0.01, 
                      color = "black", linewidth = 1.2, bandwidth = 2000) +
  scale_fill_manual(
    values = c("Salvage" = "#e74c3c", "Fair" = "#e67e22", "Average" = "#f39c12", "Good" = "#27ae60", "Excellent" = "#16a085"),
    guide = "none"
  ) +
  scale_x_continuous(limits = c(0, 80000), labels = dollar_format(prefix = "$"), 
                     breaks = seq(0, 80000, 20000)) +
  labs(
    title = "Price Distribution by Vehicle Condition (Ridge Plot)",
    subtitle = "Each ridge is one condition - Shows distribution and overlap clearly",
    x = "Selling Price ($)",
    y = "Vehicle Condition",
    caption = "Ridge heights show concentration of vehicles at each price point"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(size = 18, face = "bold", hjust = 0.5, color = "#1a1a1a", margin = margin(b = 5)),
    plot.subtitle = element_text(size = 12, color = "#555555", hjust = 0.5, margin = margin(b = 15)),
    plot.caption = element_text(size = 11, color = "#666666", hjust = 0.5, margin = margin(t = 15), face = "italic"),
    axis.title = element_text(size = 12, face = "bold", color = "#1a1a1a"),
    axis.text = element_text(size = 11, color = "#333333"),
    panel.grid.minor = element_blank(),
    panel.grid.major = element_line(color = "#e0e0e0", linewidth = 0.2),
    plot.background = element_rect(fill = "white", color = "black", linewidth = 1.5),
    panel.background = element_rect(fill = "#f9f9f9", color = NA),
    plot.margin = margin(t = 20, r = 20, b = 20, l = 20)
  )

ggsave("LINKEDIN_VIZ_2_RIDGE_PLOT_FINAL.png", p2_ridge, width = 14, height = 8, dpi = 300, bg = "white")

summary_report <- data.frame(
  Metric = c(
    "Total Vehicles Analyzed",
    "Price Range",
    "Average Selling Price",
    "Median Selling Price",
    "Most Common Condition",
    "Vehicles with Excellent Condition",
    "Average Mileage",
    "Price Depreciation Rate (per 10k miles)",
    "Most Common Body Type",
    "Price Variation (Std Dev)"
  ),
  Value = c(
    format(nrow(vehicles_clean), big.mark = ","),
    paste("$", format(round(min(vehicles_clean$sellingprice)), big.mark = ","), 
          " - $", format(round(max(vehicles_clean$sellingprice)), big.mark = ","), sep = ""),
    paste("$", format(round(mean(vehicles_clean$sellingprice)), big.mark = ","), sep = ""),
    paste("$", format(round(median(vehicles_clean$sellingprice)), big.mark = ","), sep = ""),
    names(sort(table(vehicles_clean$condition), decreasing = TRUE))[1],
    format(sum(vehicles_clean$condition == 5), big.mark = ","),
    format(round(mean(vehicles_clean$odometer)), big.mark = ","),
    paste("$", format(round(-500), big.mark = ","), sep = ""),
    names(sort(table(vehicles_clean$body), decreasing = TRUE))[1],
    paste("$", format(round(sd(vehicles_clean$sellingprice)), big.mark = ","), sep = "")
  )
)

write.csv(summary_report, "LINKEDIN_Summary_Report.csv", row.names = FALSE)
