

library(tidyverse)
library(data.table)
library(shiny)
library(kasaBasicFunctions)
library(paletter)
library(shinythemes)
library(shinycssloaders)

shinyUI(fluidPage(
  theme = shinytheme("journal"),
  titlePanel("Color extraction from a picture"),
  sidebarLayout(
    sidebarPanel(
      tags$img(
        src = "paletter_logo.png",
        width = 200,
        height = 200
      ),
      br(),
      br(),
      fileInput(
        "myFile",
        "Choose a picture file (jpg only)",
        accept = c('image/jpeg')
      ),
      numericInput('NumOfColor', 'Color count', 25, min = 1, max = 25),
      actionButton(
        inputId = "doExtration",
        label = "Extraction",
        class = "btn-primary"
      ),
      HTML("<p> &nbsp;</p><p> This website was created to make it simple to utilize"), tags$a(href = "https://github.com/AndreaCirilloAC/paletter",   "AndreaCirilloAC's paletteR R package"), HTML(".</br>Only for educational purposes.</br>")
      
    ),
    
    
    mainPanel(tabsetPanel(
      type = "tabs",
      
      tabPanel(
        plotOutput(
          outputId = "graphExample",
          width = '550px',
          height = '500px'
        ) %>% withSpinner(),
        plotOutput(
          outputId = "colorPaletter",
          width = '500px',
          height = '500px'
        ),
        htmlOutput(outputId = "colorText")
        
      )
      
    ))
  )
))
