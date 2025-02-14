# Creating-a-Scatterplot-in-R
"Create a scatterplot with a linear trendline to visualize the relationship between population density (popdensity) and the proportion of adults in the population. First, compute this proportion using popadults from the midwest dataset. Restrict the analysis to counties in Illinois.
midwest <- read.xlsx("C:/Users/Antik Debnath/Desktop/Data analytics full UIS/Copy of midwest.xlsx")
midwest %>% mutate(share_adults=popadults/poptotal) %>%
  filter(state=="IL") %>% ggplot(aes(x=popdensity, y=share_adults)) +
  geom_point()+ geom_smooth(method="lm", se=FALSE)
`geom_smooth()` using formula 'y ~ x'
0.55
data <- read.xlsx("C:Copy of NUTS2.xlsx")
data <- data %>% mutate(Country=substr(NUTS2,1,2))
cases.country <- data %>% count(Country)
data <- left_join(data,cases.country,by="Country")
data %>% filter(Country == "NO" | Country=="DE" | Country=="FR" | Country=="UK") %>%
  ggplot(aes(x=GDP,y=Patents)) + geom_point(aes(col=Country)) + theme_bw()+
  theme(legend.position = "bottom")
data <- data %>% mutate(Country=substr(NUTS2,1,2))
cases.country <- data %>% count(Country)
data <- left_join(data,cases.country,by="Country")
patents.country <- data %>% group_by(Country) %>% summarise(pat.count=sum(Patents,na.rm=T))
patents.country %>% ggplot(aes(x=reorder(as.factor(Country),-rank(pat.count)),
                               y=pat.count,fill=Country))+geom_bar(stat="identity") +
  theme_bw()+theme(legend.position = "none")+
  labs(title="Patents per European Country",x="Country",y="Number of patents")
