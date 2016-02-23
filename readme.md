# nw的require和requirejs冲突



```javascript

window.require = (function(nodewebkit, requirejs) {
    result = function(arg0) {
        if (Array.isArray(arg0)) {
            return requirejs.apply(null, arguments);
        }
        else if (arg0 == 'nw.gui') {
            return nwDispatcher.requireNwGui();
        }
        else {
            return nodewebkit.apply(null, arguments);
        }
    };
    for (var i in requirejs) {
        if (!result[i]) {
            result[i] = requirejs[i];
        }
    }
    //Simulate special require.nodeRequire, something added by r.js.
    result.nodeRequire = nodewebkit
    return result;
})(global.require, window.require);
```

from https://github.com/nwjs/nw.js/issues/422