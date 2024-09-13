library(devtools)
devtools::install_github("thiyangt/sta3262")

library(sta3262)
get_individual_project_country("AS2021563")

# get_individual_project_country("AS2021563")
# [1] "Lithuania"

library(coronavirus)
library(tidyverse)
library(broom)
library(skimr)

coronaTibble <- as_tibble(coronavirus)

# LT = Lithuania
LT_tibble <- coronaTibble %>% filter(country == "Lithuania")

LT_data <- LT_tibble %>% select(date,type,cases)

LT_data_pw <- LT_data %>% pivot_wider(names_from = type, values_from = cases) %>% 
  mutate(date = as.Date(date, format = "%Y-%m-%d"),  year = year(date)) 

LT_data_pw_clean <- LT_data_pw %>% mutate(death = ifelse(death<0,0,death),
                                          recovery = ifelse(recovery<0,0,recovery),
                                          confirmed = ifelse(confirmed<0,0,confirmed))


LT_data_pw %>%skim()

x <- LT_data_pw %>% filter(confirmed<0 | recovery < 0 | death<0)

ggplot(LT_data_pw, aes(x = date, y = confirmed)) + geom_line() + facet_grid(~year) + theme(legend.position = "bottom") + labs(title = "LT", x = "confirm" , y = "number")

LT_data_pw %>% ggplot(aes(x = date, y = confirmed)) + geom_line(color = "red")+labs(x= "Dates", y= "Confirmed cases",title = "Confirmed cases")

LT_data_pw %>%
  ggplot(aes(x = date, y = confirmed)) +
  geom_line(color = "red") +
  labs(x = "Dates", y = "Confirmed cases", title = "Confirmed cases") +
  scale_y_continuous(
    breaks = seq(0, max(LT_data_pw$confirmed), by = 2000)
  )


LT_corona_2022 <- LT_data_pw %>% filter(year == 2022)

LT_corona_2022 %>% ggplot(aes(x = date, y = confirmed)) + geom_line() + 
  labs(x= "Dates", y= "Confirmed cases",title = "Confirmed cases")


sum(LT_data_pw$death)
sum(LT_data_pw$confirmed)
summary(LT_data_pw$confirmed)

LT_data %>% filter(type %in% c("confirmed", "death")) %>% 
  ggplot(aes(x = date, y = cases, col = type)) + geom_line() + 
  labs(x = "Date", y = "Cases", title = "Cases Over Time for Selected Types") +
  theme_minimal()


# https://koronastop.lrv.lt/en/news?page=1


neighbors <- coronaTibble %>%
  filter(country %in% c("Latvia", "Belarus", "Moldova", "Poland","Lithuania")) %>% select(date,country,type,cases,lat,long) %>% pivot_wider(names_from = type, values_from = cases)

neighbors %>% ggplot(aes(x = confirmed, y = date, colour = country)) + geom_line()
hdi_index <- coronaTibble %>% filter(country %in% c("Poland","Latvia","Croatia","Bahrain","Qatar","Lithuania")) %>% select(date,country,province,type,cases,lat,long) %>% pivot_wider(names_from = type, values_from = cases)


print(hdi_index %>% filter(confirmed<0 | recovery < 0 | death<0))

print(neighbors %>% filter(confirmed<0 | recovery < 0 | death<0))


tt <- LT_data %>% group_by(type, date) %>%
  summarise(total_cases = sum(cases)) %>%
  pivot_wider(names_from = type, values_from = total_cases) %>%
  arrange(date) %>%
  mutate(active = confirmed - death - recovery) %>%
  mutate(active_total = cumsum(active),
         recovered_total = cumsum(recovery),
         death_total = cumsum(death))







library(ggplot2)
library(ggmap)
library(maps)

# Define coordinates for Lithuania
lithuania_coords <- c(lon = 23.8813, lat = 55.1694)

# Get a base map centered on Lithuania
map_data <- get_map(location = lithuania_coords, zoom = 7, maptype = "terrain")

# Plot the map with ggplot2
ggmap(map_data) +
  geom_point(aes(x = lithuania_coords["lon"], y = lithuania_coords["lat"]), color = "red", size = 4) +
  labs(title = "Map of Lithuania", x = "Longitude", y = "Latitude")


library(leaflet)
# Define coordinates for Lithuania
lithuania_lat <- 55.1694
lithuania_long <- 23.8813

# Create an interactive map centered on Lithuania
lt_map <- leaflet() %>%
  addTiles() %>%
  setView(lng = lithuania_long, lat = lithuania_lat, zoom = 7) %>%
  addMarkers(lng = lithuania_long, lat = lithuania_lat, popup = "Lithuania")


install.packages(c("sf", "rnaturalearth", "rnaturalearthdata"))

library(sf)
library(rnaturalearth)

# Get world map data
world <- ne_countries(scale = "medium", returnclass = "sf")

# Define coordinates and bounding box for Lithuania
lithuania_lat <- 55.1694
lithuania_long <- 23.8813
bbox <- c(left = 20, bottom = 50, right = 30, top = 60)  # Adjust bounds as needed

# Create a data frame for Lithuania
lithuania_df <- data.frame(
  country = "Lithuania",
  lat = lithuania_lat,
  long = lithuania_long
)

# Convert to sf object
lithuania_sf <- st_as_sf(lithuania_df, coords = c("long", "lat"), crs = 4326)

# Plot the map with adjusted bounds
ggplot(data = world) +
  geom_sf(fill = "lightgrey") +
  geom_sf(data = lithuania_sf, color = "red", size = 4) +
  coord_sf(xlim = c(bbox["left"], bbox["right"]), ylim = c(bbox["bottom"], bbox["top"]), expand = FALSE) +
  labs(title = "Map of Lithuania", x = "Longitude", y = "Latitude") +
  theme_minimal()



# Load the world map data
world_map <- map_data("world")

# Filter for Lithuania
lithuania_map <- world_map %>% filter(region == "Lithuania")

# Plot the world map
p <- ggplot() +
  geom_polygon(
    data = world_map,
    aes(x = long, y = lat, group = group),
    fill = "lightgray",
    color = "black"
  ) +
  geom_polygon(
    data = lithuania_map,
    aes(x = long, y = lat, group = group),
    fill = "slategray2",
    color = "black"
  ) +
  coord_fixed(ratio = 1.5) +  # Maintain aspect ratio
  labs(title = "World Map Highlighting Lithuania", x = "Longitude", y = "Latitude") +
  theme_minimal()

p


cc <- LT_data_pw

cc <- cc %>% mutate(death = ifelse(death<0,0,death),
                      recovery = ifelse(recovery<0,0,recovery),
                      confirmed = ifelse(confirmed<0,0,confirmed))


aws <- coronavirus %>% 
  group_by(type, date) %>%
  summarise(total_cases = sum(cases)) %>%
  pivot_wider(names_from = type, values_from = total_cases) %>%
  arrange(date) %>%
  mutate(active = confirmed - death - recovery) %>%
  mutate(active_total = cumsum(active),
         recovered_total = cumsum(recovery),
         death_total = cumsum(death))


ppp <- LT_data_pw %>% mutate(active = confirmed - death - recovery) %>%
  mutate(active_total = cumsum(active),
         recovered_total = cumsum(recovery),
         death_total = cumsum(death))


ppp %>% ggplot(aes(x = date, y = active)) + geom_line()


print(aws %>% filter(max(recovery)))

est <- coronavirus %>% filter(country == "Estonia")
