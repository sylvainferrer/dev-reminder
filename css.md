# CSS

## Appearance
``` css
input {
    appearance: none;
    -moz-appearance: none;
    -webkit-appearance: none;
}
```

## Color of the placeholder's input
``` css
::-webkit-input-placeholder { /* Chrome/Opera/Safari */
    color: pink;
}
::-moz-placeholder { /* Firefox 19+ */
    color: pink;
}
:-ms-input-placeholder { /* IE 10+ */
    color: pink;
}
:-moz-placeholder { /* Firefox 18- */
    color: pink;
}
```

## Pulse Effect

``` css
::before {
    content: "";
    position: absolute;
    z-index: 0;
    top: 50%;
    left: 50%;
    display: block;
    width: 4.75rem;
    height: 4.75rem;
    border-radius: 50%;
    background: #5f4dee;
    transform: translate(-50%,-50%);
    animation: pulse-border 1500ms ease-out infinite;
}

@keyframes pulse-border {
    0% {
        transform: translateX(-50%) translateY(-50%) translateZ(0) scale(1);
        opacity: 1;
    }
    100% {
        transform: translateX(-50%) translateY(-50%) translateZ(0) scale(1.5);
        opacity: 0;
    }
}
```

## Hover Effect

``` css
div {
box-shadow: 0 3px 5px 0 rgba(36,50,66,0.2)
}
div:hover {
  box-shadow: 0 11px 12px 0 rgba(36,50,66,0.12)
}

div {
    box-shadow: 0 10px 50px 0 rgba(84,110,122,.15);
}
div:hover {
    box-shadow: 0 10px 50px 0 rgba(84,110,122,.35);
}
```

## Nice Box Shadow

``` css
box-shadow:
    0 2.8px 2.2px rgba(0, 0, 0, 0.034),
    0 6.7px 5.3px rgba(0, 0, 0, 0.048),
    0 12.5px 10px rgba(0, 0, 0, 0.06),
    0 22.3px 17.9px rgba(0, 0, 0, 0.072),
    0 41.8px 33.4px rgba(0, 0, 0, 0.086),
    0 100px 80px rgba(0, 0, 0, 0.12)
;
```

## Layout

``` css
{% set gutter_width_percent = (16.6  * 100) / 1180 %}
{% set column_width_percent = (100 - (gutter_width_percent * 11)) / 12 %}

/* Responsive grid */
.row-fluid {display:flex;flex-wrap: wrap;}
.row-fluid [class*='span'] {margin-left: {{gutter_width_percent}}%;-webkit-box-sizing: border-box;-moz-box-sizing: border-box;-ms-box-sizing: border-box;box-sizing: border-box;}
.row-fluid [class*='span']:first-child {margin-left: 0;}
.row-fluid .span12 {flex: 0 0 auto;width: 100%}
.row-fluid .span11 {flex: 0 0 auto;width: calc( ({{column_width_percent}}% * 11) + ({{gutter_width_percent}}% * 10) );}
.row-fluid .span10 {flex: 0 0 auto;width: calc( ({{column_width_percent}}% * 10) + ({{gutter_width_percent}}% * 9) );}
.row-fluid .span9  {flex: 0 0 auto;width: calc( ({{column_width_percent}}% * 9) + ({{gutter_width_percent}}% * 8) );}
.row-fluid .span8  {flex: 0 0 auto;width: calc( ({{column_width_percent}}% * 8) + ({{gutter_width_percent}}% * 7) );}
.row-fluid .span7  {flex: 0 0 auto;width: calc( ({{column_width_percent}}% * 7) + ({{gutter_width_percent}}% * 6) );}
.row-fluid .span6  {flex: 0 0 auto;width: calc( ({{column_width_percent}}% * 6) + ({{gutter_width_percent}}% * 5) );}
.row-fluid .span5  {flex: 0 0 auto;width: calc( ({{column_width_percent}}% * 5) + ({{gutter_width_percent}}% * 4) );}
.row-fluid .span4  {flex: 0 0 auto;width: calc( ({{column_width_percent}}% * 4) + ({{gutter_width_percent}}% * 3) );}
.row-fluid .span3  {flex: 0 0 auto;width: calc( ({{column_width_percent}}% * 3) + ({{gutter_width_percent}}% * 2) );}
.row-fluid .span2  {flex: 0 0 auto;width: calc( ({{column_width_percent}}% * 2) + {{gutter_width_percent}}% );}
.row-fluid .span1  {flex: 0 0 auto;width: {{column_width_percent}}%;}

.container-fluid .row-fluid .wrapper,
.wrapper {
	margin: 0 auto;
	max-width: var(--wrapper-max-width);
	padding: var(--wrapper-padding)
}

@media (max-width: 768px) {
  .row-fluid [class*='span'] {
	  margin-left: 0;
		flex-shrink: 0;
		width: 100%;
		max-width: 100%}
}
```
