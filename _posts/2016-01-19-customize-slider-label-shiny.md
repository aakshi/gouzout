---
title: "How to customize slide labels in Shiny"
layout: post
---
[Shiny](http://shiny.rstudio.com/) offers a good selection of arguments to help you customize the slider input control. If you need to add a prefix or suffix to a label it's easy to do in R. But, if you need more complicated reformating of labels Javascript is your friend.

Looking at the Shiny source code we can see that Shiny uses the [Ion Range Slider](http://ionden.com/a/plugins/ion.rangeSlider/en.html) JQuery component.

The Ion Range Slider has a number of additional settings we can tap into. To customize the rendering of the labels we're going to use the Ion Range Slider `prettify` setting which allows us to use a callback function to render our labels.

Create a Javascript file in your Shiny project called `slider.js`.

```javascript
$(document).ready(function() {

  function createLabel(num) {
    //Some sort of transformation happens here
    return label;
  }
  
  /**
  Tweak ionRangeSlider options
  prettify tells the ionRangeSlider to 
  use our createLabel function to
  render the slider labels
  */
  var slider = $("#sliderOne").ionRangeSlider({
    prettify: createLabel,
  });
})
```

Next the custom Javascript needs to be added to the Shiny app using the `includeScript` function to the `ui.R` file.

```r

library(shiny)

shinyUI(fluidPage(  
  # Adds custom JS to head of Shiny HTML page
  tags$head(includeScript('slider.js')),
))
```

Finally, the range slide component needs to be added the Shiny `ui.R` file.

{% marginnote 'mn-id-r-code-2' '*Note:* the first argument for the sliderInput *sliderOne* matches the id used in the Javascript file.' %}

```r

library(shiny)

shinyUI(fluidPage(  
  # Adds custom JS to head of Shiny HTML page
  tags$head(includeScript('slider.js')),

  verticalLayout(
    wellPanel(
      sliderInput("sliderOne",
                  "Slider with fancy labels:",
                  min = 0,
                  max = 47,
                  value = 24)
    ),
  ),
))
```

See a full implementation of this technique on [Github](https://github.com/richshaw/timeUse).


