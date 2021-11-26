### R snippets to access Socrata-based open data servers (Example 1)
##### Description
This example creates a map viewer by pulling a dataset from the NYC’s Open Data Portal containing a list of NYC Health and Hospitals Corporation Facilities

##### Code
```r
library("RSocrata") # reading and writing to and from Socrata

# human-readable URL
url <- "https://data.cityofnewyork.us/Health/NYC-Health-and-Hospitals-Corporation-Facilities/ymhw-9cz9"

df.hhc <- read.socrata(url)

# type conversion
df.hhc$Facility.Name <- as.character(df.hhc$Facility.Name)
df.hhc$Cross.Streets <- as.character(df.hhc$Cross.Streets)
df.hhc$Phone <- as.character(df.hhc$Phone)
df.hhc$Location.1 <- as.character(df.hhc$Location.1)

# data parsing to extract location 
extract_location <- function(x) 
    return <- unlist(gsub("[\\(\\)]", "", regmatches(x, gregexpr("\\(.*?\\)", x))[[1]]))

extract_latlon <- function(x) 
    return (unlist(strsplit(x, ", ")))

extract_lat <- function(x) 
    return (as.numeric(x[1]))

extract_lon <- function(x) 
    return (as.numeric(x[2]))

location <- lapply(df.hhc$Location.1, function(x) extract_location(x))
location <- lapply(location, function(x) extract_latlon(x[[1]]))

df.hhc$Lat <- sapply(location, function(x) extract_lat(x))
df.hhc$Lon <- sapply(location, function(x) extract_lon(x))

# add the leaflet library to your script
library(leaflet)

# Similar to addCircleMarkers(addTitle(leaflet()))
leaflet(data = df.hhc) %>%
    addTiles() %>%
        addCircleMarkers(
            ~Lon, ~Lat, popup = ~as.character(Facility.Name), clusterOptions = markerClusterOptions())
```


### R snippets to access Socrata-based open data servers (Example 2)
##### Description
This example creates a map viewer (clustering) by pulling a dataset from the NYC’s Open Data Portal containing a list of NYC Health and Hospitals Corporation Facilities.

##### Code
```r

library("RSocrata") # reading and writing to and from Socrata

# human-readable URL
url <- "https://data.cityofnewyork.us/Health/NYC-Health-and-Hospitals-Corporation-Facilities/ymhw-9cz9"

df.hhc <- read.socrata(url)

# type conversion
df.hhc$Facility.Name <- as.character(df.hhc$Facility.Name)
df.hhc$Cross.Streets <- as.character(df.hhc$Cross.Streets)
df.hhc$Phone <- as.character(df.hhc$Phone)
df.hhc$Location.1 <- as.character(df.hhc$Location.1)

# data parsing to extract location 
extract_location <- function(x) 
    return <- unlist(gsub("[\\(\\)]", "", regmatches(x, gregexpr("\\(.*?\\)", x))[[1]]))

extract_latlon <- function(x) 
    return (unlist(strsplit(x, ", ")))

extract_lat <- function(x) 
    return (as.numeric(x[1]))

extract_lon <- function(x) 
    return (as.numeric(x[2]))

location <- lapply(df.hhc$Location.1, function(x) extract_location(x))
location <- lapply(location, function(x) extract_latlon(x[[1]]))

df.hhc$Lat <- sapply(location, function(x) extract_lat(x))
df.hhc$Lon <- sapply(location, function(x) extract_lon(x))

# add the leaflet library to your script
library(leaflet)

# Create a palette that maps factor levels to colors
pal <- colorFactor(c("navy", "red", "orange", "purple"), domain = df.hhc$Facility.Type)

map <- leaflet(data = df.hhc) %>% 
    addTiles(group = "OSM (default)") %>%
    addProviderTiles("Stamen.Toner", group = "Toner") %>%
    addProviderTiles("Stamen.TonerLite", group = "Toner Lite") %>%
    addCircleMarkers(
        ~Lon, ~Lat,
        color = ~pal(Facility.Type),
        stroke = FALSE, 
          fillOpacity = 0.5,
        popup= ~as.character(Facility.Name),
        group = "HHC"
    ) %>%
     # Layers control
    addLayersControl(
        baseGroups = c("OSM (default)", "Toner", "Toner Lite"),
        overlayGroups = c("HHC"),
        options = layersControlOptions(collapsed = FALSE)
)
map
```

### R snippets to access CKAN-based open data servers
##### Description
This example is pulling a dataset from the CivicData Open Data Portal containing 2014 Salt Lake City crime incidents.

##### Code
```r
url <- "http://civicdataprod1.cloudapp.net/storage/f/2014-07-07T16%3A17%3A25.958Z/2014.csv"

crimes <- read.csv(file=url,head=TRUE,sep=",")
nrow(crimes)
head(crimes)
str(crimes)

# type conversion
crimes$Address <- as.character(crimes$Address)
crimes$Description <- as.character(crimes$Description)

str(crimes)
# levels to groups data
table(crimes$Type)

library(leaflet)

num_colors <- length(levels(crimes$Type))
pal <- colorFactor(topo.colors(num_colors), crimes$Type)

map <- leaflet(data = crimes) %>% 
    addTiles(group = "OSM (default)") %>%
    addProviderTiles("Stamen.Toner", group = "Toner") %>%
    addProviderTiles("Stamen.TonerLite", group = "Toner Lite") %>%
    addCircleMarkers(
        ~Longitude, ~Latitude,
        color = ~pal(Type),
        stroke = FALSE, 
        fillOpacity = 0.5,
        popup= ~as.character(Description),
        group = "Crimes"
    ) %>%
    # Layers control
    addLayersControl(
        baseGroups = c("OSM (default)", "Toner", "Toner Lite"),
        overlayGroups = c("Crimes"),
        options = layersControlOptions(collapsed = FALSE)
    )
map
```