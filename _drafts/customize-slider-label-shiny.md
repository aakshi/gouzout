---
title: "How to customize slide labels in Shiny"
layout: post
---
[Shiny](http://shiny.rstudio.com/) offers a great selection of arguments to help you customize the slider input control. If you need to add a prefix or suffix to a label it's easy to do in R, but if you need to do more complicated reformating of labels then you need to work with Javascript.

## Example

We have a dataset that labels each 30 minute period during the day from 0 to 47 and we want to convert these integer to a time range. For example 1 = 12:30am to 1:00am.

{% marginnote 'mn-id-example-table' '*Table 1*: Example dataset' %}
<div class="table-wrapper">
<table>
    <thead>
        <tr><th>sex</th><th>agegrp</th><th>activity</th><th>b0</th><th>b1</th><th>b2</th></tr>
    </thead>
    <tbody>
        <tr><td>male</td><td>5</td><td>10101</td><td>0.919</td><td>0.932</td><td>0.947</td></tr>
        <tr><td>female</td><td>3</td><td>10101</td><td>0.897</td><td>0.921</td><td>0.944</td></tr>
        <tr><td>female</td><td>5</td><td>10101</td><td>0.891</td><td>0.918</td><td>0.944</td></tr>
        <tr><td>female</td><td>2</td><td>10101</td><td>0.887</td><td>0.911</td><td>0.944</td></tr>
        <tr><td>male</td><td>4</td><td>10101</td><td>0.892</td><td>0.916</td><td>0.936</td></tr>
        <tr><td>female</td><td>4</td><td>10101</td><td>0.867</td><td>0.9</td><td>0.93</td></tr>
        <tr><td>female</td><td>1</td><td>10101</td><td>0.888</td><td>0.906</td><td>0.929</td></tr>
        <tr><td>male</td><td>3</td><td>10101</td><td>0.883</td><td>0.904</td><td>0.927</td></tr>
        <tr><td>female</td><td>0</td><td>10101</td><td>0.817</td><td>0.846</td><td>0.896</td></tr>
    </tbody>
</table>
</div>

## Custom JS

Looking at the Shiny source code we can see that Shiny uses the [Ion Range Slider](http://ionden.com/a/plugins/ion.rangeSlider/en.html) JQuery component.

The Ion Range Slider has a number of additional settings we can hack into. To customize the rendering of the labels we're going to use the Ion Range Slider `prettify` setting which allows us to use a callback function to render our labels.

Create a Javascript file in your Shiny project called `slider.js`.

```javascript
$(document).ready(function() {

  var now = new Date();
  var now_bin = now.getHours() * 2; // bin number, 30-minute bins
  if (now.getMinutes() >= 30) {
    now_bin += 1;
  }

  /**
  Function to convert bin numbers 0 to 47 
  to time segments in words.

  This is an example you can use whatever 
  function you like to render your labels.  
  */
  function binNumberToWords(bin_num) {
    var hour = Math.floor(bin_num / 2);
    if (bin_num == now_bin) {
    return 'Right Now';
    } else if (hour > 12) {
    ampm_start = "pm";
    ampm_finish = "pm";
    hour -= 12;
    } else if (hour == 0) {
    ampm_start = "am";
    ampm_finish = "am";
    hour = 12;
    } else if (hour == 12) {
    ampm_start = "pm";
    ampm_finish = "pm";
    } else {
    ampm_start = "am";
    ampm_finish = "am";
    }
    var remainder = bin_num % 2;
    if (remainder > 0) {
    var time_span = hour + ":30"+ampm_start+"-" + hour + ":59"+ampm_finish;
    } else {
    var time_span = hour + ":00"+ampm_start+"-" + hour + ":29"+ampm_finish; 
    }
    
    return time_span;
  }
  
  /**
  Tweak ionRangeSlider options
  prettify tells the ionRangeSlider to 
  use our binNumberToWords function to
  render the slider labels
  */
  var slider = $("#timeOfDay").ionRangeSlider({
    prettify: binNumberToWords,
  });
})
```

Next we need to add our custom Javascript to our Shiny app using the `includeScript` function. To your `ui.R` file add.

```r
library(shiny)

shinyUI(fluidPage(  
  # Adds custom JS to head of Shiny HTML page
  tags$head(includeScript('slider.js')),
))
```

Finally, the range slide component needs to be added the Shiny <ui.R> file.

{% marginnote 'mn-id-r-code-2' '*Note:* the first argument for the sliderInput *timeOfDay* matches the id used in the Javascript file.' %}

```r
library(shiny)
shinyUI(fluidPage(  
  # Adds custom JS to head of Shiny HTML page
  tags$head(includeScript('slider.js')),

  verticalLayout(
    wellPanel(
      sliderInput("timeOfDay",
                  "Time of day:",
                  min = 0,
                  max = 47,
                  value = 24),
      selectInput("sex",
                  "Sex:",
                  c("Males" = "male",
                    "Females" = "female"),
                  selected = "male"),
      selectInput("ageGrp", "Age:",
                  c("15 to 24" = 0,
                    "25 to 34" = 1,
                    "35 to 44" = 2,
                    "45 to 54" = 3,
                    "55 to 64" = 4,
                    "65+" = 5),
                  selected = 2)
    ),
  ),
))
```

See the full implementation of this technique on [Github](https://github.com/richshaw/timeUse).


