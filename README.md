# javascript30
30 day JS Projects challenge

First project in the JS30 challenge.

This Drum Kit project helped me to practice and improve upon:
1) Key events
2) The transitionEnd and animationEnd event listeners
3) Playing audio
4) Implementing logic

There are no improvements or upgrades slated for this project. 

A walkthrough of the JS with brief summary is below:

First a function needed to be created which would be able to create sound for the specified keys. This was done using data-key and key class on the divs containing the notes. The audio.currentTime=0 allows for fast repeats to be possible and the playing class adds the yellow border box to active keys. const audio creates the sound and const key matches the sounds to their respective key. 
```JavaScript
 function playSound(e){
    
    const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
    const key = document.querySelector(`.key[data-key="${e.keyCode}"]`);
    if(!audio) return;
    audio.currentTime = 0; //rewind to the start
    audio.play();
    key.classList.add('playing');
  }
```

Next we needed to remove the transition style that was just added to the active keys. Remember that this. is referring to the key because the key is where the event listener is located and this keyword always takes the object that it is listening on. 
```JavaScript
  function removeTransition(e){
    if(e.propertyName !== 'transform') return; //skip it if its not a tranform
    this.classList.remove('playing');
  }
```

With const keys we made an array of .key class holders and looped through it adding a transitionend listener to every key in the array which will remove the transiton that was just applied.
```JavaScript
  const keys = document.querySelectorAll('.key');
  keys.forEach(key => key.addEventListener('transitionend', removeTransition));
```

```JavaScript
window.addEventListener('keydown', playSound);
```
