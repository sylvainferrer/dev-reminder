# JavaScript

## Swipe Detection

```javascript
document.addEventListener('touchstart', handleTouchStart, false);
document.addEventListener('touchmove', handleTouchMove, false);

var xDown = null;
var yDown = null;

function getTouches(evt) {
  return evt.touches ||             // browser API
         evt.originalEvent.touches; // jQuery
}

function handleTouchStart(evt) {
    const firstTouch = getTouches(evt)[0];
    xDown = firstTouch.clientX;
    yDown = firstTouch.clientY;
};

function handleTouchMove(evt) {
    if ( ! xDown || ! yDown ) {
        return;
    }

    var xUp = evt.touches[0].clientX;
    var yUp = evt.touches[0].clientY;

    var xDiff = xDown - xUp;
    var yDiff = yDown - yUp;

    if ( Math.abs( xDiff ) > Math.abs( yDiff ) ) {/*most significant*/
        if ( xDiff > 0 ) {
            /* left swipe */ 
        } else {
            /* right swipe */
        }
    } else {
        if ( yDiff > 0 ) {
            /* up swipe */ 
        } else { 
            /* down swipe */
        }
    }
    /* reset values */
    xDown = null;
    yDown = null;
};
```

## Copy current URL to clipboard
```javascript
function insertSuccessPopup() {
    const successDiv = document.createElement('div');
    successDiv.textContent = "URL Copied";
    successDiv.setAttribute('class', 'success-div');
    document.body.append(successDiv);
    setTimeout(() => {
        successDiv.classList.add('fade-out');
        setTimeout(() => {
            successDiv.remove();
        }, 500)
    }, 2500)
}
const shares = document.querySelectorAll(".blogpost__share-link");
if (shares.length > 0) {
    shares.forEach(share => {
        share.addEventListener('click', () => {
            const tempInput = document.createElement('input');
            const url = location.href;
            tempInput.value = url;
            document.body.append(tempInput);
            tempInput.select();
            document.execCommand("copy");
            tempInput.remove();
            insertSuccessPopup();
        })
    })
}
```