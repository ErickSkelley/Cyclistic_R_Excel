# Rides by Day of Week





### Members vs Casual Riders

```r
ggplot(data = Divvy_Q1) +
  geom_bar(mapping = aes(x = day_of_week), fill = "slategray") +
  facet_wrap(~member_casual,
             labeller = labeller(member_casual = c(
               "member" = "Annual Members",
               "casual" = "Casual Riders")))+
  labs(x = "Days of the Week",
       y = "Total Trips")+
  scale_y_continuous(labels = label_number(scale = 1e-3, suffix = "K"))+
  scale_x_continuous(breaks = c(1:7),
                     labels = c("Sunday","Monday","Tuesday","Wednesday","Thursday","Friday",
                                "Saturday"))
```






### Casual Riders

```r
Divvy_Q1 %>%
  filter(member_casual == "casual")%>%
  ggplot(data=.)+
  geom_bar(mapping = aes(x = day_of_week), fill = "slategray") +
  labs(title = "Casual Users Rides by Day",
       x = "Days of the Week",
       y = "Total Trips")+
  scale_y_continuous(labels = label_number(scale = 1e-3, suffix = "K"))+
  scale_x_continuous(breaks = c(1:7),
                     labels = c("Sunday","Monday","Tuesday","Wednesday","Thursday","Friday",
                                "Saturday"))
```




---

# Ride Length by User Type


### Casual

```r
Divvy_Q1 %>%
  filter(member_casual == "casual")%>%
  ggplot(data = .)+
  geom_histogram(aes(x = ride_length_sec), fill = "slategray") +
  scale_x_continuous(limits = c(0, 4000))+
  labs(
    title = "Ride Length by Casual Riders",
    x = "Ride Length (seconds)",
    y = "Total Trips")+
  scale_y_continuous(labels = label_number(scale = 1e-3, suffix = "K"))
```


### Members

```r
Divvy_Q1 %>%
  filter(member_casual == "member")%>%
  ggplot(data = .)+
  geom_histogram(aes(x = ride_length_sec), fill = "slategray") +
  scale_x_continuous(limits = c(0, 4000))+
  labs(
    title = "Ride Length by Member",
    x = "Ride Length (seconds)",
    y = "Total Trips")+
  scale_y_continuous(labels = label_number(scale = 1e-3, suffix = "K"))
```


---


# Top 10 Starting Stations for Casual Riders

### Create New Table

```r
top_start_casual <- Divvy_Q1 %>%
  filter(member_casual == "casual")%>%
  count(start_station_name, sort = TRUE) %>%
  slice_head(n = 10)
```






### New Table As Chart

```r
ggplot(data = top_start_casual)+
  geom_point(aes(x=total_starts,y=reorder(start_station_name,total_starts)), color = "darkblue",size = 4)+
  labs(
    title = "Top 10 Start Stations (Casual)",
    x = "Total Trips from Station",
    y = " ")+
  theme(axis.text.y = element_text(face = "bold"))+
  theme(axis.text.x = element_text(face = "bold"))
```
