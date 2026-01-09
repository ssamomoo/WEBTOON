# WEBTOON DEA
Naver Webtoon Data Exploratory Analysis

# Summary:
Using R Studio and Google's Cloud Translation API, I put together an exploratory analysis of Naver Webtoon's top stories of the year 2024. 
I was able to use my personal Korean language knowledge to translate the columns with smaller, repeating words like genre and age rating. 

    naverwebtoon<-read.csv("naver.csv")
    genre_translation <- list(
      "일상" = "daily",
      "코믹" = "comic",
      "드라마" = "drama",
      "감성" = "emotional",
      "힐링" = "healing",
      "개그" = "gag",
      "스릴러" = "thriller",
      "액션" = "action",
      "로맨스"= "romance",
      "판타지" = "fantasy",
      "스포츠" = "sports",
      "에피소드" = "episode",
      "옴니버스" = "omnibus",
      "스토리" = "story",
      "무협" = "martial arts",
      "사극" = "historical")
    
    age_translation <- list(
      "전체연령가" = "all ages",
      "12세 이용가" = "12+",
      "15세 이용가" = "15+",
      "18세 이용가" = "18+")
    translate_genres <- function(g, dictionary) {
      parts <- unlist(strsplit(g, ","))
      translated <- sapply(parts, function(x) dictionary[[trimws(x)]] %||% trimws(x))
      paste(translated, collapse = ", ")}
    naverwebtoon$genre_en <- sapply(naverwebtoon$genre, translate_genres, dictionary = genre_translation)
    head(naverwebtoon[, c("genre", "genre_en")])
    translate_age <- function(age, dictionary) {
      parts <- unlist(strsplit(age, ","))
      translated <- sapply(parts, function(x) dictionary[[trimws(x)]] %||% trimws(x))
      paste(translated, collapse = ", ")}
    naverwebtoon$age_en <- sapply(naverwebtoon$age, translate_age, dictionary = age_translation)
    head(naverwebtoon[, c("age", "age_en")])

Using Google's Cloud API, I was able to translate the longer columns like description, title, and author. Using the now trnaslated columns, I wrote them onto an entirely new translated dataset.

