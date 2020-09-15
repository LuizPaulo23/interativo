# interativo
Plotando gráfico de dispersão interativo 

######## Pacote Necessário ##############
library(gganimate)
library(ggplot2)

###### Plotando o gráfico de dipersão com a relação entre o índice de Gini e Taxa de Alfabetização (2000-2010) ####  

grafico <- base %>%
  ggplot() + 
  geom_point(aes(x = base$Taxa_Alfabetizacao, y = base$Gini,
                 col = Mesorregioes), alpha = 0.8) + theme_minimal() + 
  theme(legend.position = "bottom") + guides(size = "none") + 
  labs(x = "Taxa de Alfabetização" ,y = "Índice de Gini",  col = "")
grafico +
  geom_text(aes(x = min(base$Taxa_Alfabetizacao), y = min(base$Gini),label = as.factor(Year)),
            hjust=-2, vjust = -0.2, alpha = 0.2,  col = "black", size = 20) +
  transition_states(as.factor(Year), state_length = 0)

##### Para salvar ####
getwd()
meu_gif<-animate(grafico, duration=15)
save_animation(animation = meu_gif, file = "medium.gif")

