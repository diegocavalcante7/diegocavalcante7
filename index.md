## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/diegocavalcante7/diegocavalcante7/edit/gh-pages/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/diegocavalcante7/diegocavalcante7/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

---
title: "Ãndice de confianÃ§a nas instituiÃ§Ãµes democrÃ¡ticas"
author: "DIEGO CAVALCANTE e YURY MACHADO"
date: "05/12/2020"
output: ioslides_presentation
code_folding: hide
---

```{r setup, echo=FALSE}
knitr::opts_chunk$set(echo = FALSE)
```

```{r Load, echo=FALSE, message=FALSE, warning=FALSE, paged.print=FALSE}

lapply(c("tidyverse","haven","lubridate",
         "janitor","readxl","moderndive", "ggplot2",
         "stringr", "magrittr","srvyr",
         "survey"),require,character.only=T)
library(tidyverse)
library(ggplot2)
library(readxl)
library(foreign)
library(scales)
library(moderndive)
library(infer)
library(psy)
```
## Justificativa TeÃ³rica

Uma das caracterÃ­sticas fundamentais para a criaÃ§Ã£o e manutenÃ§Ã£o de uma instituiÃ§Ã£o o reconhecimento de sua legitimidade.


Para instituiÃ§Ãµes que constituem as democracias liberais comtemporÃ¢neas, como as CÃ¢maras Legislativas, o JudiciÃ¡rio, os partidos polÃ­ticos e o executivo, Ã©  fundamental que os cidadÃ£os reconheÃ§am as instituiÃ§Ãµes como pilares do sistema democrÃ¡tico, e por isso, garantidoras de seus direitos e liberdades.

No entanto, Ã© possÃ­vel observar que discursos que deslegitimam tais instituiÃ§Ãµes vem crescendo no Brasil, em especial ao considerarmos que o presidente eleito em 2018 possui um histÃ³rico de crÃ­ticas ao poder legislativo e ao Supremo Tribunal Federal, algo que continuou se manifestando apÃ³s sua posse.

## Justificativa TeÃ³rica

Portanto, torna-se de grande interesse para a ciÃªncia polÃ­tica analisar o quanto esses discursos estÃ£o presentes na opniÃ£o pÃºblica.


ste trabalho visa a realizaÃ§Ã£o dessa tarefa a partir do banco de dados do Estudo Eleitoral Brasileiro (ESEB), usando uma questÃ£o que indaga o quanto o entrevistado confia nas instituiÃ§Ãµes citadas acima, e dessa forma, criar um Ã­ndice de confianÃ§a nas instituiÃ§Ãµes democrÃ¡ticas.

O grÃ¡fico exposto na prÃ³xima sessÃ£o Ã© o produto desse Ã­ndice.
```{r}
Eseb2018 <- read_dta("ESEB2018.dta")

Eseb2018 %>%       
  select(P404, P405, P407, P408) %>% 
  cronbach()
categorias <- c()
lvl_trust2 <-  Eseb2018 %>%       
  select(P404, P405, P407, P408) %>% 
  mutate(trust = P404 + P405 + P407 + P408)%>%
  filter(trust <= 16)
```
## GrÃ¡fico
```{r, echo=FALSE, warning=FALSE}
lvl_trust2 %>% 
  ggplot(aes(x = trust)) +
  geom_histogram( binwidth = 2, boundary = 1, color = "darkblue", fill="lightblue") +
  scale_y_continuous(limits = c(0, 800), breaks = breaks_width(100))+
  scale_x_continuous(breaks = breaks_width(100))+ 
  geom_vline(aes(xintercept=mean(trust)),
             color="orange", size=1.5)+
  geom_vline(aes(xintercept=median(trust)),
             color="red", size=1.5)+
  geom_text(aes(x=12.8, label="MÃ©dia", y=775), colour="orange", text=element_text(size=11)) +
  geom_text(aes(x=11.3, label="Mediana", y=775), colour="red", text=element_text(size=11))+
  scale_fill_manual(name="Linhas verticais",values=c("red","orange"),labels=c("Mediana","MÃ©dia"))+
  labs(x = "Muita ConfianÃ§a             Alguma confianÃ§a                  Pouca confianÃ§a         Nenhuma confianÃ§a", title="ConfianÃ§a nas instituiÃ§Ãµes democrÃ¡ticas")
```




### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
