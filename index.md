---
framework: basedemo
highlighter: prettify
hitheme: twitter-bootstrap
mode: selfcontained
--- &nav

- [Item 1](item1)
- [Item 2](item2)
- .download [Item 3](item3)

--- &header version:v1

## BaseDemo 

BaseDemo is just a basic template that can be used for creating demos for your development projects. It also works great for GitHub Pages. This is an example of what you could do with this template and some content types.





<style>iframe {width: 100%; height: 350px;}</style>

--- &demo

## Example One

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vestibulum pellentesque risus id eros semper non eleifend lorem imperdiet. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae; Aliquam fermentum sapien non nibh consectetur elementum.

*** .active #1

## Code


```r
require(rCharts)
options(RCHART_WIDTH = 650, RCHART_HEIGHT = 300)
r1 <- rPlot(mpg ~ wt, data = mtcars, type = 'point')
r1
```



*** #2

## Result

<iframe src=assets/fig/unnamed-chunk-1.html seamless></iframe>


--- &demo .RAW

## Slide Layouts

*** #c1 .active

## Slide


```
--- .class1 #id1 bg:yellow

## Slide Title

Slide Contents
```


*** #c2

## Parsed


```
$html
[1] "<h2>Slide Title</h2>\n\n<p>Slide Contents</p>\n"

$header
[1] "<h2>Slide Title</h2>"

$level
[1] "2"

$title
[1] "Slide Title"

$content
[1] "<p>Slide Contents</p>\n"

$id
[1] "id1"

$bg
[1] "yellow"

$class
[1] "class1"
```



*** #c3

## Layout



```
<slide class="{{ slide.class }}" id="{{ slide.id }}" style="background:{{{ slide.bg }}};">
  {{# slide.header }}
  <hgroup>
    {{{ slide.header}}}
  </hgroup>
  {{/ slide.header }}
  <article data-timings="{{ slide.dt }}">
    {{{ slide.content }}}
  </article>
  <!-- Presenter Notes -->
  {{# slide.pnotes }}
  <aside class="note" id="{{ id }}">
    <section>
      {{{ html }}}
    </section>
  </aside>
  {{/ slide.pnotes }}
</slide>
```



*** #c4

## Rendered


```
<slide class="class1" id="id1" style="background:yellow;">
  <hgroup>
    <h2>Slide Title</h2>
  </hgroup>
  <article data-timings="">
    <p>Slide Contents</p>

  </article>
  <!-- Presenter Notes -->
</slide>
```



*** #c5

## View

<slide class="class1" id="id1" style="background:yellow;">
  <hgroup>
    <h2>Slide Title</h2>
  </hgroup>
  <article data-timings="">
    <p>Slide Contents</p>

  </article>
  <!-- Presenter Notes -->
</slide>







