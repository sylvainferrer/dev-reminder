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