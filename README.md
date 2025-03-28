
<!-- README.md is generated from README.Rmd. Please edit the README.Rmd file -->

# Lab report \#3 - instructions

Follow the instructions posted at
<https://ds202-at-isu.github.io/labs.html> for the lab assignment. The
work is meant to be finished during the lab time, but you have time
until Monday evening to polish things.

Include your answers in this document (Rmd file). Make sure that it
knits properly (into the md file). Upload both the Rmd and the md file
to your repository.

All submissions to the github repo will be automatically uploaded for
grading once the due date is passed. Submit a link to your repository on
Canvas (only one submission per team) to signal to the instructors that
you are done with your submission.

# Lab 3: Avenger’s Peril

## As a team

Extract from the data below two data sets in long form `deaths` and
`returns`

``` r
av <- read.csv("https://raw.githubusercontent.com/fivethirtyeight/data/master/avengers/avengers.csv", stringsAsFactors = FALSE)
head(av)
```

    ##                                                       URL
    ## 1           http://marvel.wikia.com/Henry_Pym_(Earth-616)
    ## 2      http://marvel.wikia.com/Janet_van_Dyne_(Earth-616)
    ## 3       http://marvel.wikia.com/Anthony_Stark_(Earth-616)
    ## 4 http://marvel.wikia.com/Robert_Bruce_Banner_(Earth-616)
    ## 5        http://marvel.wikia.com/Thor_Odinson_(Earth-616)
    ## 6       http://marvel.wikia.com/Richard_Jones_(Earth-616)
    ##                    Name.Alias Appearances Current. Gender Probationary.Introl
    ## 1   Henry Jonathan "Hank" Pym        1269      YES   MALE                    
    ## 2              Janet van Dyne        1165      YES FEMALE                    
    ## 3 Anthony Edward "Tony" Stark        3068      YES   MALE                    
    ## 4         Robert Bruce Banner        2089      YES   MALE                    
    ## 5                Thor Odinson        2402      YES   MALE                    
    ## 6      Richard Milhouse Jones         612      YES   MALE                    
    ##   Full.Reserve.Avengers.Intro Year Years.since.joining Honorary Death1 Return1
    ## 1                      Sep-63 1963                  52     Full    YES      NO
    ## 2                      Sep-63 1963                  52     Full    YES     YES
    ## 3                      Sep-63 1963                  52     Full    YES     YES
    ## 4                      Sep-63 1963                  52     Full    YES     YES
    ## 5                      Sep-63 1963                  52     Full    YES     YES
    ## 6                      Sep-63 1963                  52 Honorary     NO        
    ##   Death2 Return2 Death3 Return3 Death4 Return4 Death5 Return5
    ## 1                                                            
    ## 2                                                            
    ## 3                                                            
    ## 4                                                            
    ## 5    YES      NO                                             
    ## 6                                                            
    ##                                                                                                                                                                              Notes
    ## 1                                                                                                                Merged with Ultron in Rage of Ultron Vol. 1. A funeral was held. 
    ## 2                                                                                                  Dies in Secret Invasion V1:I8. Actually was sent tto Microverse later recovered
    ## 3 Death: "Later while under the influence of Immortus Stark committed a number of horrible acts and was killed.'  This set up young Tony. Franklin Richards later brought him back
    ## 4                                                                               Dies in Ghosts of the Future arc. However "he had actually used a hidden Pantheon base to survive"
    ## 5                                                      Dies in Fear Itself brought back because that's kind of the whole point. Second death in Time Runs Out has not yet returned
    ## 6                                                                                                                                                                             <NA>

``` r
str(av)
```

    ## 'data.frame':    173 obs. of  21 variables:
    ##  $ URL                        : chr  "http://marvel.wikia.com/Henry_Pym_(Earth-616)" "http://marvel.wikia.com/Janet_van_Dyne_(Earth-616)" "http://marvel.wikia.com/Anthony_Stark_(Earth-616)" "http://marvel.wikia.com/Robert_Bruce_Banner_(Earth-616)" ...
    ##  $ Name.Alias                 : chr  "Henry Jonathan \"Hank\" Pym" "Janet van Dyne" "Anthony Edward \"Tony\" Stark" "Robert Bruce Banner" ...
    ##  $ Appearances                : int  1269 1165 3068 2089 2402 612 3458 1456 769 1214 ...
    ##  $ Current.                   : chr  "YES" "YES" "YES" "YES" ...
    ##  $ Gender                     : chr  "MALE" "FEMALE" "MALE" "MALE" ...
    ##  $ Probationary.Introl        : chr  "" "" "" "" ...
    ##  $ Full.Reserve.Avengers.Intro: chr  "Sep-63" "Sep-63" "Sep-63" "Sep-63" ...
    ##  $ Year                       : int  1963 1963 1963 1963 1963 1963 1964 1965 1965 1965 ...
    ##  $ Years.since.joining        : int  52 52 52 52 52 52 51 50 50 50 ...
    ##  $ Honorary                   : chr  "Full" "Full" "Full" "Full" ...
    ##  $ Death1                     : chr  "YES" "YES" "YES" "YES" ...
    ##  $ Return1                    : chr  "NO" "YES" "YES" "YES" ...
    ##  $ Death2                     : chr  "" "" "" "" ...
    ##  $ Return2                    : chr  "" "" "" "" ...
    ##  $ Death3                     : chr  "" "" "" "" ...
    ##  $ Return3                    : chr  "" "" "" "" ...
    ##  $ Death4                     : chr  "" "" "" "" ...
    ##  $ Return4                    : chr  "" "" "" "" ...
    ##  $ Death5                     : chr  "" "" "" "" ...
    ##  $ Return5                    : chr  "" "" "" "" ...
    ##  $ Notes                      : chr  "Merged with Ultron in Rage of Ultron Vol. 1. A funeral was held. " "Dies in Secret Invasion V1:I8. Actually was sent tto Microverse later recovered" "Death: \"Later while under the influence of Immortus Stark committed a number of horrible acts and was killed.'"| __truncated__ "Dies in Ghosts of the Future arc. However \"he had actually used a hidden Pantheon base to survive\"" ...

``` r
summary(av)
```

    ##      URL             Name.Alias         Appearances       Current.        
    ##  Length:173         Length:173         Min.   :   2.0   Length:173        
    ##  Class :character   Class :character   1st Qu.:  58.0   Class :character  
    ##  Mode  :character   Mode  :character   Median : 132.0   Mode  :character  
    ##                                        Mean   : 414.1                     
    ##                                        3rd Qu.: 491.0                     
    ##                                        Max.   :4333.0                     
    ##     Gender          Probationary.Introl Full.Reserve.Avengers.Intro
    ##  Length:173         Length:173          Length:173                 
    ##  Class :character   Class :character    Class :character           
    ##  Mode  :character   Mode  :character    Mode  :character           
    ##                                                                    
    ##                                                                    
    ##                                                                    
    ##       Year      Years.since.joining   Honorary            Death1         
    ##  Min.   :1900   Min.   :  0.00      Length:173         Length:173        
    ##  1st Qu.:1979   1st Qu.:  5.00      Class :character   Class :character  
    ##  Median :1996   Median : 19.00      Mode  :character   Mode  :character  
    ##  Mean   :1988   Mean   : 26.55                                           
    ##  3rd Qu.:2010   3rd Qu.: 36.00                                           
    ##  Max.   :2015   Max.   :115.00                                           
    ##    Return1             Death2            Return2             Death3         
    ##  Length:173         Length:173         Length:173         Length:173        
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##    Return3             Death4            Return4             Death5         
    ##  Length:173         Length:173         Length:173         Length:173        
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##    Return5             Notes          
    ##  Length:173         Length:173        
    ##  Class :character   Class :character  
    ##  Mode  :character   Mode  :character  
    ##                                       
    ##                                       
    ## 

Get the data into a format where the five columns for Death\[1-5\] are
replaced by two columns: Time, and Death. Time should be a number
between 1 and 5 (look into the function `parse_number`); Death is a
categorical variables with values “yes”, “no” and ““. Call the resulting
data set `deaths`.

Similarly, deal with the returns of characters.

Based on these datasets calculate the average number of deaths an
Avenger suffers.

``` r
deaths <- av %>%
  select(Name.Alias, starts_with("Death")) %>%
  pivot_longer(
    cols = starts_with("Death"),
    names_to = "Time",
    values_to = "Death"
  ) %>%
  mutate(
    Time = parse_number(Time),
    Death = tolower(trimws(Death))
  )         

head(deaths)
```

    ## # A tibble: 6 × 3
    ##   Name.Alias                     Time Death
    ##   <chr>                         <dbl> <chr>
    ## 1 "Henry Jonathan \"Hank\" Pym"     1 "yes"
    ## 2 "Henry Jonathan \"Hank\" Pym"     2 ""   
    ## 3 "Henry Jonathan \"Hank\" Pym"     3 ""   
    ## 4 "Henry Jonathan \"Hank\" Pym"     4 ""   
    ## 5 "Henry Jonathan \"Hank\" Pym"     5 ""   
    ## 6 "Janet van Dyne"                  1 "yes"

``` r
tail(deaths)
```

    ## # A tibble: 6 × 3
    ##   Name.Alias  Time Death
    ##   <chr>      <dbl> <chr>
    ## 1 Ava Ayala      5 ""   
    ## 2 Kaluu          1 "no" 
    ## 3 Kaluu          2 ""   
    ## 4 Kaluu          3 ""   
    ## 5 Kaluu          4 ""   
    ## 6 Kaluu          5 ""

``` r
str(deaths)
```

    ## tibble [865 × 3] (S3: tbl_df/tbl/data.frame)
    ##  $ Name.Alias: chr [1:865] "Henry Jonathan \"Hank\" Pym" "Henry Jonathan \"Hank\" Pym" "Henry Jonathan \"Hank\" Pym" "Henry Jonathan \"Hank\" Pym" ...
    ##  $ Time      : num [1:865] 1 2 3 4 5 1 2 3 4 5 ...
    ##  $ Death     : chr [1:865] "yes" "" "" "" ...

``` r
deaths
```

    ## # A tibble: 865 × 3
    ##    Name.Alias                     Time Death
    ##    <chr>                         <dbl> <chr>
    ##  1 "Henry Jonathan \"Hank\" Pym"     1 "yes"
    ##  2 "Henry Jonathan \"Hank\" Pym"     2 ""   
    ##  3 "Henry Jonathan \"Hank\" Pym"     3 ""   
    ##  4 "Henry Jonathan \"Hank\" Pym"     4 ""   
    ##  5 "Henry Jonathan \"Hank\" Pym"     5 ""   
    ##  6 "Janet van Dyne"                  1 "yes"
    ##  7 "Janet van Dyne"                  2 ""   
    ##  8 "Janet van Dyne"                  3 ""   
    ##  9 "Janet van Dyne"                  4 ""   
    ## 10 "Janet van Dyne"                  5 ""   
    ## # ℹ 855 more rows

``` r
returns <- av %>%
  pivot_longer(cols = starts_with("Return"),
               names_to = "Time",
               values_to = "Return") %>%
  mutate(Time = parse_number(Time),
         Return = tolower(Return))

head(returns)
```

    ## # A tibble: 6 × 18
    ##   URL                 Name.Alias Appearances Current. Gender Probationary.Introl
    ##   <chr>               <chr>            <int> <chr>    <chr>  <chr>              
    ## 1 http://marvel.wiki… "Henry Jo…        1269 YES      MALE   ""                 
    ## 2 http://marvel.wiki… "Henry Jo…        1269 YES      MALE   ""                 
    ## 3 http://marvel.wiki… "Henry Jo…        1269 YES      MALE   ""                 
    ## 4 http://marvel.wiki… "Henry Jo…        1269 YES      MALE   ""                 
    ## 5 http://marvel.wiki… "Henry Jo…        1269 YES      MALE   ""                 
    ## 6 http://marvel.wiki… "Janet va…        1165 YES      FEMALE ""                 
    ## # ℹ 12 more variables: Full.Reserve.Avengers.Intro <chr>, Year <int>,
    ## #   Years.since.joining <int>, Honorary <chr>, Death1 <chr>, Death2 <chr>,
    ## #   Death3 <chr>, Death4 <chr>, Death5 <chr>, Notes <chr>, Time <dbl>,
    ## #   Return <chr>

``` r
tail(returns)
```

    ## # A tibble: 6 × 18
    ##   URL                 Name.Alias Appearances Current. Gender Probationary.Introl
    ##   <chr>               <chr>            <int> <chr>    <chr>  <chr>              
    ## 1 http://marvel.wiki… Ava Ayala           49 YES      FEMALE ""                 
    ## 2 http://marvel.wiki… Kaluu               35 YES      MALE   ""                 
    ## 3 http://marvel.wiki… Kaluu               35 YES      MALE   ""                 
    ## 4 http://marvel.wiki… Kaluu               35 YES      MALE   ""                 
    ## 5 http://marvel.wiki… Kaluu               35 YES      MALE   ""                 
    ## 6 http://marvel.wiki… Kaluu               35 YES      MALE   ""                 
    ## # ℹ 12 more variables: Full.Reserve.Avengers.Intro <chr>, Year <int>,
    ## #   Years.since.joining <int>, Honorary <chr>, Death1 <chr>, Death2 <chr>,
    ## #   Death3 <chr>, Death4 <chr>, Death5 <chr>, Notes <chr>, Time <dbl>,
    ## #   Return <chr>

``` r
str(returns)
```

    ## tibble [865 × 18] (S3: tbl_df/tbl/data.frame)
    ##  $ URL                        : chr [1:865] "http://marvel.wikia.com/Henry_Pym_(Earth-616)" "http://marvel.wikia.com/Henry_Pym_(Earth-616)" "http://marvel.wikia.com/Henry_Pym_(Earth-616)" "http://marvel.wikia.com/Henry_Pym_(Earth-616)" ...
    ##  $ Name.Alias                 : chr [1:865] "Henry Jonathan \"Hank\" Pym" "Henry Jonathan \"Hank\" Pym" "Henry Jonathan \"Hank\" Pym" "Henry Jonathan \"Hank\" Pym" ...
    ##  $ Appearances                : int [1:865] 1269 1269 1269 1269 1269 1165 1165 1165 1165 1165 ...
    ##  $ Current.                   : chr [1:865] "YES" "YES" "YES" "YES" ...
    ##  $ Gender                     : chr [1:865] "MALE" "MALE" "MALE" "MALE" ...
    ##  $ Probationary.Introl        : chr [1:865] "" "" "" "" ...
    ##  $ Full.Reserve.Avengers.Intro: chr [1:865] "Sep-63" "Sep-63" "Sep-63" "Sep-63" ...
    ##  $ Year                       : int [1:865] 1963 1963 1963 1963 1963 1963 1963 1963 1963 1963 ...
    ##  $ Years.since.joining        : int [1:865] 52 52 52 52 52 52 52 52 52 52 ...
    ##  $ Honorary                   : chr [1:865] "Full" "Full" "Full" "Full" ...
    ##  $ Death1                     : chr [1:865] "YES" "YES" "YES" "YES" ...
    ##  $ Death2                     : chr [1:865] "" "" "" "" ...
    ##  $ Death3                     : chr [1:865] "" "" "" "" ...
    ##  $ Death4                     : chr [1:865] "" "" "" "" ...
    ##  $ Death5                     : chr [1:865] "" "" "" "" ...
    ##  $ Notes                      : chr [1:865] "Merged with Ultron in Rage of Ultron Vol. 1. A funeral was held. " "Merged with Ultron in Rage of Ultron Vol. 1. A funeral was held. " "Merged with Ultron in Rage of Ultron Vol. 1. A funeral was held. " "Merged with Ultron in Rage of Ultron Vol. 1. A funeral was held. " ...
    ##  $ Time                       : num [1:865] 1 2 3 4 5 1 2 3 4 5 ...
    ##  $ Return                     : chr [1:865] "no" "" "" "" ...

``` r
avg_deaths <- deaths %>%
  group_by(Name.Alias) %>%
  summarize(num_deaths = sum(Death =="yes", na.rm = TRUE)) %>%
  ungroup() %>%
  summarize(average_deaths = mean(num_deaths))

avg_deaths
```

    ## # A tibble: 1 × 1
    ##   average_deaths
    ##            <dbl>
    ## 1          0.546

``` r
debug_deaths <- deaths %>%
  group_by(Name.Alias) %>%
  summarize(num_deaths = sum(Death == "yes", na.rm = TRUE))

print(debug_deaths)
```

    ## # A tibble: 163 × 2
    ##    Name.Alias              num_deaths
    ##    <chr>                        <int>
    ##  1 ""                               7
    ##  2 "\"Giulietta Nefaria\""          1
    ##  3 "Adam"                           1
    ##  4 "Adam Brashear"                  0
    ##  5 "Alani Ryan"                     0
    ##  6 "Alex Summers"                   0
    ##  7 "Alexis"                         0
    ##  8 "Alias: Jonas"                   1
    ##  9 "Amadeus Cho"                    0
    ## 10 "America Chavez"                 0
    ## # ℹ 153 more rows

## On average each Avenger experiences 0.5460123 deaths.

## Individually - Brandon Merrick

### FiveThirtyEight Statement

> Given the Avengers’ 53 years in operation and overall mortality rate,
> fans of the comics can expect one current or former member to die
> every seven months or so, with a permanent death occurring once every
> 20 months.

### Include the code

``` r
operation_time <- 53 * 12
total_deaths <- deaths %>% summarise(num_deaths = sum(Death == "yes", na.rm = TRUE))
avg_time_between_deaths <- operation_time / total_deaths
permanent_deaths <- sum(returns$Return == "no")
avg_time_between_permanent_deaths <- operation_time / permanent_deaths
avg_time_between_deaths
```

    ##   num_deaths
    ## 1   7.146067

``` r
avg_time_between_permanent_deaths
```

    ## [1] 19.875

### Include your answer

The data shows that there is a death every 7.15 months and a permanent
death every 19.875 months. These numbers round to the whole numbers
given in the article so although not exact the article is accurate.

## Individually - Lucas

### FiveThirtyEight Statement

> There’s a 2-in-3 chance that a member of the Avengers returned from
> their first stint in the afterlife, but only a 50 percent chance they
> recovered from a second or third death.

### Include the code

``` r
av_long <- av %>%
   pivot_longer(cols = matches("Death[1-5]|Return[1-5]"),
                names_to = c(".value", "Time"),
                names_pattern = "(Death|Return)([1-5])") %>%
  mutate(across(c(Death, Return), tolower),
         Time = as.numeric(Time))

first_return_rate <- av_long %>%
  filter(Time == 1, Death == "yes") %>%
  summarize(
    total_died_first = n(),
    total_returned_first = sum(Return == "yes", na.rm = TRUE),
    percent_returned_first = (total_returned_first  / total_died_first) * 100
    )

second_third_return_rate <- av_long %>%
  filter(Time %in% c(2,3), Death == "yes") %>%
  summarize(
    total_died_second_third = n(),
    total_returned_second_third = sum(Return == "yes", na.rm = TRUE),
    percent_returned_second_third = (total_returned_second_third / total_died_second_third) * 100
  )

first_return_rate
```

    ## # A tibble: 1 × 3
    ##   total_died_first total_returned_first percent_returned_first
    ##              <int>                <int>                  <dbl>
    ## 1               69                   46                   66.7

``` r
second_third_return_rate
```

    ## # A tibble: 1 × 3
    ##   total_died_second_third total_returned_second_third percent_returned_second_…¹
    ##                     <int>                       <int>                      <dbl>
    ## 1                      18                           9                         50
    ## # ℹ abbreviated name: ¹​percent_returned_second_third

### Include your answer

The fact-check confirms that the statement is accurate: **exactly
66.7%** of Avengers returned after their first death, and precisely
**50.0%** returned from their second or third deaths, matching the
original claim.

## Individually - Nina

### FiveThirtyEight Statement

> I counted 89 total deaths — some unlucky Avengers7 are basically Meat
> Loaf with an E-ZPass — and on 57 occasions the individual made a
> comeback.

### Include the code

``` r
#Nina

sum(deaths$Death == "yes", na.rm = TRUE)
```

    ## [1] 89

``` r
#Nina

sum(returns$Return == "yes", na.rm = TRUE)
```

    ## [1] 57

### Include your answer

Above is my work to show fact-checking that there is a total of 89
deaths, and 57 returns. I fact checked this by using the sum function to
add up the number of times the option “yes” occurs in the variable
Death. Similarly, I used the sum function to add up the number of times
“yes” appears in the Return column.
