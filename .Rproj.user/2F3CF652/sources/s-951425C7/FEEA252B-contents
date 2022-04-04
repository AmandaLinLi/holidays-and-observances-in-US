#' Date 2022/04/04
#' Author Amanda Li

library(dplyr)

#' Goal

#' A data frame with date and names of holidays and observances in the US over the next years (2022-2030)

# date        holiday
# 2022-01-01  New Year’s Day
# 2022-01-17  Martin Luther King Jr. Day


#' function that extracts holidays and observances in the US over the next years (2022-2030)
#'  using website scraping from 'https://www.timeanddate.com/holidays/us/?hol=313'
#' @param url vector of URLs of the website that contains the holiday data
#' @param year sequence of target years
#' return a tibble containing the info shown in the goal

extract_holidays <- function(url = url, year = year) {
  page <- url %>% rvest::read_html()

  raw <- page %>%
    {
      data.frame(
        tbl = rvest::html_node(., "table") %>% rvest::html_node(., "tbody") %>%
          rvest::html_nodes(., "tr") %>%
          rvest::html_children() %>%
          rvest::html_text()
      )
    } %>%
    mutate(tbl = trimws(tbl, "both"))

  tibble(
    year = year,
    date = raw %>%
      slice(seq(1, nrow(.), 5)) %>%
      pull(tbl) %>%
      as.Date(format = "%b%d") %>%
      as.character() %>%
      stringr::str_replace(string = ., pattern = "2022", as.character(year)),
    holiday = raw %>%
      slice(seq(3, nrow(.), 5)) %>%
      pull(tbl)
  ) %>%
    unique()
}
