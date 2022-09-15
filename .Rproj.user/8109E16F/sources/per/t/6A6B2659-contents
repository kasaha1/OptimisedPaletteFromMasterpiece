

library(tidyverse)
library(data.table)
library(shiny)
library(shinycssloaders)
library(kasaBasicFunctions)
library(paletter)

options(shiny.maxRequestSize = 300 * 1024 ^ 2)

shinyServer(function(input, output) {
  uploadedImage <- reactive({
    inFile <- input$myFile
    if (is.null(inFile))
      return()
    return(inFile$datapath)
  })
  DoPrediction <- observeEvent(input$doExtration, {
    output$graphExample <- renderPlot(NA)
    
    b64 <- base64enc::dataURI(file = uploadedImage(), mime = "image/png")
    insertUI(
      selector = "#image-container",
      where = "afterBegin",
      ui = img(src = b64, width = 200, height = 200)
    )
    
    NumColor <- input$NumOfColor
    
    MTcars <- mtcars[1:NumColor, ]
    
    output$colorPaletter <- renderPlot(
      colours_vector <<-
        create_palette(
          image_path = uploadedImage(),
          number_of_colors = NumColor,
          type_of_variable = "categorical"
        )
    )
    output$colorText <-
      renderText(paste(shQuote(colours_vector), collapse = ", "))
    output$graphExample <-
      renderPlot(
        ggplot(
          data = MTcars,
          aes(
            x = rownames(MTcars),
            y = hp,
            color = rownames(MTcars),
            fill = rownames(MTcars)
          )
        ) +
          scale_color_manual(values = colours_vector) +
          scale_fill_manual(values = colours_vector) +
          geom_bar(stat = 'identity') +
          theme_minimal() +
          guides(size = "none") +
          theme(legend.position = "bottom") +
          labs(title = "disp vs hp") +
          coord_flip()
      )
  })
  MTcars_d <- mtcars[1:25, ]
  output$graphExample <-
    renderPlot(
      ggplot(
        data = MTcars_d,
        aes(
          x = rownames(MTcars_d),
          y = hp,
          color = rownames(MTcars_d),
          fill = rownames(MTcars_d)
        )
      ) +
        geom_bar(stat = 'identity') +
        theme_minimal() +
        guides(size = "none") +
        theme(legend.position = "bottom") +
        labs(title = "disp vs hp") +
        coord_flip()
    )
})
