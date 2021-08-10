# UCSB General Education Courses 2021-2022

This data compiles all GE courses for 2021-2022 which meet the following requirements:

* Area B: Foreign Language
* Area C: Science, Mathematics, and Technology
* Area D: Social Sciences
* Area E: Culture and Thought
* Area F: Arts
* Area G: Literature
* Ethnicity: Ethnicity
* Euro Trad: European Traditions
* Quant. Relationships: Quantitative Relations
* World Cult: World Cultures
* Writing: Writing
* AHI: American History and Institutions
* IGETC Category: Credit for transfer students

Note that list does not include Area A, however these courses are easy to identify from the numbers, and do not overlap with any other course on this list.

This data was compiled from the [Degree Requirements](https://duels.ucsb.edu/advising/planning/degree#Area%20A:%20%20English%20Reading%20and%20Composition) page, converted using an [online converter](https://smallpdf.com/pdf-to-excel) and cleaned using the R code below.

```R
ge <- read.csv("ge_data.csv")
colnames(ge) <- ge[1,]
ge <- ge[-1,-1]
ge$Course <- str_replace_all(
  str_match(
    ge$Course,
    "^[^\\d]*\\d+(\\w\\d)*"
  )[,1], 
  "(\\s|\\t)+",
  " "
)
ge[,2:ncol(ge)] <- ifelse(ge[,2:ncol(ge)] == "", 0, 1)
```