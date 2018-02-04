Topic: Event Listeners
Date: 1/4/18
***


"Bubbling up"
Instead of using a for loop to add event listeners to multiple contained elements, you can set the listener to the parent.

Add an if statement to exlude the parent in the event.

```javascript
function gridEvents() {
  const grid = document.getElementById('grid');

  const cell1 = document.createElement('div');
  cell1.className = 'cell';
  cell1.innerText = 1;
  const cell2 = document.createElement('div');
  cell2.className = 'cell';
  cell2.innerText = 2;
  const cell3 = document.createElement('div');
  cell3.className = 'cell';
  cell3.innerText = 3;

  // cell3.onclick = colorBg;
  // cell3.onmouseleave = backToWhite;

  grid.addEventListener('click', colorBg);
  grid.addEventListener('mouseout', backToWhite);

  function colorBg(e) {
    if (e.target !== grid) {
      changeBgColor('#f00', e.target);
    }
  }

  function backToWhite(e) {
    console.log(e.target)
    changeBgColor('#fff', e.target);
  }

  function changeBgColor(color, target) {
    target.style.backgroundColor = color;
  }
  // cell1.addEventListener('click', function (event) {
  //   console.log(event.target.innerText);
  // });

  // cell1.addEventListener('click', function (event) {
  //   console.log('boo');
  // })

  // cell1.addEventListener('click', clickHandler);

  // cell1.addEventListener('mouseover', function (event) {
  //   console.log(event.target)
  // })

  // function clickHandler(event) {
  //   console.log('handler fired', event.target);
  // }
  // cell1.onclick = function (event) {
  //   console.log(event);
  // }
  // cell2.onclick = function (event) {
  //   console.log('clicked on ' + event.target.innerText + '!');
  // }
  grid.appendChild(cell1);
  grid.appendChild(cell2);
  grid.appendChild(cell3);

}

gridEvents();
```