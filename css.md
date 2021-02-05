# CSS

## Appearance
``` css
appearance: none;
-moz-appearance: none;
-webkit-appearance: none;
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
::before {    content: "";    position: absolute;    z-index: 0;    top: 50%;    left: 50%;    display: block;    width: 4.75rem;    height: 4.75rem;    border-radius: 50%;    background: #5f4dee;    animation: pulse-border 1500ms ease-out infinite;    transform: translate(-50%,-50%);
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