library(dplyr)
source("R/function.R")
year <- 2023:2030
left <- rep("https://www.timeanddate.com/holidays/us/", 2030 - 2023 + 1)
right <- rep("?hol=313", 2030 - 2023 + 1)

urls <- c(
  "https://www.timeanddate.com/holidays/us/?hol=313",
  paste0(left, year, right, sep = "")
)


res <- purrr::map2_dfr(
  urls, 2022:2030,
  ~ extract_holidays(url = .x, year = .y)
) %>%
  dplyr::nest_by(year)

qs::qsave(res,"data/outputs/US-hol-obs(2022-2030).qs")
write.csv(tidyr::unnest(res,cols = c(data)) ,"data/outputs/US-hol-obs(2022-2030).csv")
