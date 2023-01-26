Output all your console log (log, debug, info, warn, error) in a Div on your website

![image](https://user-images.githubusercontent.com/67203548/214893631-5297a189-750f-4e60-9f5a-16126b95dad5.png)

Javascript code:
```js
var log = document.getElementsByClassName('consoleOutput')[0];
['log', 'debug', 'info', 'warn', 'error'].forEach(function (verb) {
    console[verb] = (function (method, verb, log) {
        return function () {
            method.apply(console, arguments);
            for (const argument of arguments) {
                let msg = document.createElement('code');
                msg.classList.add(verb);
                msg.textContent = verb + ': ' + argument;
                log.appendChild(msg);
            }
        };
    })(console[verb], verb, log);
});


console['clear'] = (function (method, verb, log) {
    return function () {
        method.apply(console, arguments);
        log.innerHTML = '';
    };
})(console['clear'], 'clear', log);
clear = console.clear;
```
