
## Инструкция
### Как забрать модель.
  1. Идём на Hero Forge, загружаем персонажа
  2. Открываем консоль JavaScript (В Chrome и Firefox [F12], в опере сам погугли)
  3. Вставляем код снизу
  4. Жмём Энтер и сверху на странице появятся кнопки .stl и .obj. Скачиваем .obj. Quality не трогаем, оно должно быть 0.
  ### А как запихнуть в Tabletop? Мне пишет Failed to load!111 Ажтрисёт!!
  5. Скачанную модель просто так запихнуть в Tabletop обычно нельзя. Придётся запихать в любой 3D редактор, повернуть модель вертикально, Weld (Сварить вместе) вершины с минимальным порогом (например 0,001 мм) и уменьшить количество полигонов модификатором ProOptimizer так чтобы вершин было меньше 20 000, желательно около 15 000 или типа того. (Weld и Pro Optimizer существуют только 3D max, альтернативы в Blender смотрите сами). 
  6. Экспортируем модель как .obj. Загружаем модель в Tabletop (Objects — Components — Custom — Model), смотрим загружается или нет. Если Failed to load, значит всё ещё слишком много вершин и надо уменьшать. 
  7. Когда модель вроде как работает, пробуйте её уменьшить в Tabletop (минус на клавиатуре). Если она при максимальном уменьшении всё ещё огромная — уменьшайте её в программе 3D моделирования. Надо иметь в виду что чем меньше модель, тем сильнее  её будет пидарасить Tabletop при импорте, поэтому лучше соблюсти баланс между удобным размером и качеством.
  8. Наконец, делаем коллайдер. Ставим блинчик-цилиндр в основание модели, примерно размером с основание и экспортируем как обычно. Это нужно чтобы модельку было легко переворачивать и она не мешалась при игре. 
  9. Усё.


### Код снизу.
```
var xhr=new XMLHttpRequest;xhr.open("get","https://raw.githubusercontent.com/AugustBebel/Buttface/master/dist/saver.min.js",true);xhr.onreadystatechange=function(){if(xhr.readyState==4){var script=document.createElement("script");script.type="text/javascript";script.text=xhr.responseText;document.body.appendChild(script)}};xhr.send(null);
```

### Loading via Greecemonkey or other script loader
This method should automatically load the script on page load. 

1. Install Greasemonkey Browser Addon (or alternative)
2. [Click here to install](https://raw.githubusercontent.com/TeaWithLucas/Herosaver/master/herosaver-autoloader.user.js "Click to install"), Link to repository: [herosaver-autoloader.user.js](herosaver-autoloader.user.js)
3. The install window should pop up, check "Open editor after install completes" if you want to add domains, then click install.
4. If it doesn't pop up an install window, either Greasemonkey isn't installed or another problem has occured, you can try adding the script manually.

## User Guide

### Buttons
* STL - Exports the current model and downloads a STL of it.
* OBJ - Exports the current model and downloads a OBJ of it.

### Options
* Quality - Number of loop subdivision passes for the model.

### Dropdown Menu Items
* Save - Exports the current model settings in a JSON format.
* Load - Imports a previously exported JSON file with model settings.

## Limitations

* This is a collaborative effort by people of the community, so the output is not perfect. 
* If you want higher quality exports, consider purchasing the stl files or help work on the code :)
* The outputted file is not a solid object, but a set of objects which is fine for some uses, but can be problimatic if you want to print the 3D object. You will probabily need to combine these into a solid ojbect, Consider using [Meshmixer](http://www.meshmixer.com/download.html "Meshmixer Download Link") (or equvilient) to produce a printable output, some guides below.

## 3D Printing Guides

For some guides look at:
* [Youtube - Master Miniatures with Meshmixer Supports](https://www.youtube.com/watch?v=8xY2gHLg-ZA "Youtube - Master Miniatures with Meshmixer Supports")
* [Youtube - How to create custom supports in Meshmixer](https://www.youtube.com/watch?v=OXFKVmMwXCQ "Youtube - How to create custom supports in Meshmixer")
* [Reddit - Cheatsheet on Printing and Painting Miniatures](https://www.reddit.com/r/PrintedMinis/comments/8c0uvr/cheatsheet_on_printing_and_painting_miniatures/ "Cheatsheet on Printing and Painting Miniatures")
* [Reddit - A detailed guide to printing your minis](https://www.reddit.com/r/PrintedMinis/comments/8c0uvr/cheatsheet_on_printing_and_painting_miniatures/ "A detailed guide to printing your minis")

## Contributing

### Installing minifyer
1. [Install NPM](https://www.npmjs.com/get-npm)
2. Clone the repository
3. Navigate to the repository in your console
4. Install rollup using:
```
npm install rollup
```
### Minifying
1. Navigate to the repository in your console
2. Build the minified version using:
```
npm run build
```

## Bugs

Current bugs, open to solutions/suggestions
* Shaders are not included, causing a more _'blocky'_ output, work on the THREE.js section is needed for this.

## Future work

Current things to work on, open to solutions/suggestions
* Empty?

## Done

### Finished work

* Rotation is off by 90 degrees, simple fix
* The buttons for enlarge and reset scale are a quick and ugly method, needs reworking to not affect the scale in brower if possible, if not, automatically change scale when downloading and resetting scale when downloaded. My lack of THREE.js experience means I am unsure how to do the latter.

### Fixed bugs

* Reset Scale Button doesnt work first press, need a second refresh to work.
* Autoloader.js doesnt work when page is reloaded, only on first page load.
* Some Geometry like facial experessions are not implemented, need to work on the THREE.js section.
