# E.T.L-with-Power-Query
Extract Transforma and Load data using Power Query
# INTRO
The general sequence in any analytic project involves Extracting, Transforming and Loading data. It is however common place in most to focus solely in the transforming and Loading aspect of the sequence and leaving the part of extraction to the Data Engineers.
Extracting seems to be an ardous task because of the tools and skills involved agreed, but it is a skill that should be learnt.
In this project the Data science book portfolio from Ebay was extracted using Power Query, transformed and loaded for analysis but focus is mainly on the Extraction.
# Steps in extraction
*Find walk through video here: https://youtu.be/J3AYIkYg9Qs*
# Abridged explanation of the video
*  Connect to web
*  Get table by example (on each column start typing the row field that you require and powerBI will auto populate)
*  Load for transformation
*  PowerBI will load only the forst page from the web page so you will have iterate through the required pages to do,
  *  on the formular bar, create a variable *=(StartPage)=>*
  *  In the Query script replace the page number with *StartPage*

{ 
  = (StartPage)=>
let
    Source = Web.BrowserContents("https://www.ebay.com/sch/i.html?_from=R40&_nkw=Data+science&_sacat=261186&_pgn="&StartPage),
    #"Extracted Table From Html" = Html.Table(Source, {{"Book Title", ".srp-river-results .s-item__title"}, {"Price", ".srp-river-results .s-item__price"}, {"shipping from", ".s-item__location"}, {"shipping price", ".s-item__shipping"}}, [RowSelector=".s-item\-\-watch-at-corner"]),
    #"Changed Type" = Table.TransformColumnTypes(#"Extracted Table From Html",{{"Book Title", type text}, {"Price", Currency.Type}, {"shipping from", type text}, {"shipping price", type text}})
in
    #"Changed Type" 
    }

