# U.S. Flight Delays & Reliability Dashboard (June 2003–March 2020)

## Project Overview

This project analyzes U.S. flight delay patterns and their relationship with weather hazards to help travelers make informed decisions about which airports to use or avoid during adverse weather conditions. The analysis examines 17 years of flight data to identify which airports are most affected by weather-related delays and cancellations.

## Data Source

The dataset used in this analysis comes from Kaggle: [Airline Delay Causes](https://www.kaggle.com/datasets/anshuls235/airline-delay-causes)

This comprehensive dataset contains flight statistics for U.S. airports from June 2003 to March 2020, including detailed delay information broken down by cause (weather, carrier, NAS, security, and late aircraft).

## Data Dictionary

The following table describes all variables used in this analysis:

| Variable | Description |
|----------|-------------|
| `airport` | IATA code for the airport |
| `airport_name` | Full name of the airport |
| `AirportFullName` | Complete airport name with city information |
| `City_State_Country` | Geographic location of the airport |
| `arr_cancelled` | Number of cancelled arrival flights |
| `arr_delay` | Total minutes of arrival delays |
| `arr_diverted` | Number of diverted arrival flights |
| `arr_flights` | Total number of arrival flights |
| `arr_del15` | Number of flights delayed 15+ minutes on arrival |
| `carrier` | Airline carrier code |
| `carrier_name` | Full airline name |
| `carrier_delay` | Minutes delayed due to carrier issues |
| `carrier_issue_rate` | Percentage of flights delayed due to carrier |
| `avg_delay_min_per_delayed_flight` | Average delay in minutes for delayed flights |
| `avg_delay_min_per_flight` | Average delay across all flights |
| `Delay Bucket` | Categorization of delay severity (Low, Medium, High) |
| `late_aircraft_delay` | Minutes delayed due to late arriving aircraft |
| `late_aircraft_issue_rate` | Percentage of flights delayed due to late aircraft |
| `nas_delay` | Minutes delayed due to National Airspace System issues |
| `nas_issue_rate` | Percentage of flights delayed due to NAS |
| `pct_cancelled` | Percentage of flights cancelled |
| `pct_cancelled_15plus` | Percentage of flights cancelled with 15+ min delays |
| `pct_diverted` | Percentage of flights diverted |
| `security_delay` | Minutes delayed due to security issues |
| `security_issue_rate` | Percentage of flights delayed due to security |
| `share_delay_carrier` | Proportion of delays caused by carrier |
| `share_delay_late_aircraft` | Proportion of delays caused by late aircraft |
| `share_delay_nas` | Proportion of delays caused by NAS |
| `share_delay_security` | Proportion of delays caused by security |
| `share_delay_weather` | Proportion of delays caused by weather |
| `weather_delay` | Minutes delayed due to weather conditions |
| `weather_issue_rate` | Percentage of flights delayed due to weather |

## Database Architecture

The data was processed and analyzed using SQLite, with three main tables created:

### Table 1: `flights_data`
Contains raw flight information including airport codes, flight counts, cancellations, and diversions. This table stores the foundational metrics for all arriving and departing flights.

### Table 2: `airport_efficiency_metrics`
Aggregates delay metrics by airport and includes calculated fields for delay impact analysis, including the Delay Bucket categorization used for visualization.

### Table 3: `airport_parsed`
Enhances the efficiency metrics with additional geographic information (city, state, country) and provides the complete dataset for dashboard integration.

### ODBC Connection
An ODBC (Open Database Connectivity) connection was established to enable seamless data transfer between the SQLite database and Microsoft Power BI. This connection allows for real-time data refresh and interactive dashboard querying without duplicating the source data.

### Database Schema Diagram

![SQLite Database Tables Schema](Tables%20SQL.jpg)

## Dashboard Visualization

![Flight Delays Dashboard](Dashboard%20Image%20Flights%20US.jpg)

![Weather-Related Delays Dashboard View](Dashboard%20Image%20Weather-Related.jpg)

### Dashboard Overview


The interactive dashboard presents four key visualizations:

1. **Delay Rate by Month (with Median)** - Line chart showing delay trends throughout the year with both actual rates and median values, helping identify seasonal patterns.

2. **Annual Flight Arrivals with Delays Highlighted** - Stacked bar chart comparing total arrivals against delayed flights by year, illustrating the scale of the problem over time.

3. **High-Traffic Airports vs. Delay Impact** - Scatter plot displaying each airport's total flight volume against its delay rate, identifying which airports experience the worst delay problems relative to their traffic.

4. **Geographic Heatmap** - Interactive U.S. map showing delay severity by region, with color-coded delay buckets (green = low, yellow = medium, orange/red = high).

### Key Metrics Displayed

- **Avg. Flights Delayed per Month**: 59.09K flights
- **% of Flights Delayed**: 18.59% 
- **Avg. Delay per Delayed Flight**: 58.73 minutes

### Weather-Related Delays Metrics

The dashboard also provides a focused view on weather-related delays specifically, which helps travelers understand the impact of weather conditions:

- **Avg. Flights Delayed per Month (Weather-Related)**: 1.80K flights
- **% of Flights Delayed (Weather-Related)**: 0.57%
- **Avg. Delay per Delayed Flight (Weather-Related)**: 86.15 minutes

*Note: While weather causes only a small percentage of delays (0.57%), the average delay duration for weather-affected flights (86.15 minutes) is significantly higher than the overall average (58.73 minutes), indicating that weather delays tend to be more severe when they occur.*


### How Travelers Can Use This Dashboard

This dashboard is designed to help travelers make informed decisions when planning flights:

- **Route Planning**: Identify high-delay airports to avoid if possible, or select alternative routes
- **Timing Optimization**: Understand seasonal delay patterns to schedule travel during lower-delay months
- **Carrier Selection**: See which airports/carriers have better reliability records
- **Risk Assessment**: Know which airports are most susceptible to weather disruptions
- **Weather Awareness**: During severe weather warnings, check if your departure/arrival airport is in a high-delay-risk region

## Important Disclaimers

### Weather Delay vs. Cancellation Paradox

⚠️ **Critical Context**: While only 2-3% of flights are officially recorded as delayed due to weather conditions, **significantly more flights are cancelled during severe weather events**. This is an important distinction:

- A flight marked as "weather delayed" typically experiences delays up to 2-3 hours that airline operations can manage
- Flights are **cancelled** (not counted in delay metrics) when weather makes operations unsafe or impossible
- During major storms, cancellation rates can spike dramatically, affecting far more passengers than the delay statistics suggest

**Source**: [FAA Flight Delay Information](https://www.faa.gov/data_research/aviation_data_statistics/traffic_flows_airports/) and industry research on storm-related disruptions

### Data Limitations

- This analysis covers June 2003 through March 2020 and may not reflect current airport operations
- Delay data represents official airline reporting and may not capture full customer experience impacts
- Weather severity is inferred from delay patterns, not direct meteorological data
- Regional patterns may vary significantly based on seasonal weather patterns

## Future Enhancements

- Integration of real-time weather data with flight delay predictions
- Machine learning models to predict flight delays based on weather forecasts
- Comparison analysis with post-2020 data to assess changes in airport reliability
- Expansion to international flight patterns
