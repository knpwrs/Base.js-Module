# Base.js Module
This is a modular version of Dean Edward's [Base.js](http://dean.edwards.name/weblog/2006/03/base/). The same script will work the same in CommonJS Environments (such as [node.js](http://nodejs.org/)), AMD Environments (such as [RequireJS](http://requirejs.org/)), and plain browser environments.

In addition to modularizing the code I have also updated the entire implementation so that it passes [JSHint](http://www.jshint.com/) (with default settings in the installed version -- the web version turns on `strict` by default).

# Getting Started
The first way to get started using the script is to simply include it wherever else you include scripts (be it at the top, bottom, through a script loader, or what have you):

  <script src="/path/to/Base.js"></script>

The second way to get started is to include the script as a dependency for an AMD application or module (using something such as [RequireJS](http://requirejs.org/)):

    require('/path/to/Base', function (Base) {
      // You may now use Base.js as "Base" here.
    });

The third and final way to get started is to `require` the module in a CommonJS environment (such as [node.js](http://nodejs.org/)):

    var Base = require('./path/to/Base');

If you are using [node.js](http://nodejs.org/) with [npm](http://npmjs.org) then you can also install the module as follows:

    npm install basejs

Then in your script you only need to do the following:

    var Base = require('basejs');

# Defining Classes
Moving forward, whichever path you chose above you should now have a `Base` object to work with. Basic usage is as follows:

    // Define Animal class
    var Animal = Base.extend({
      constructor: function (name) {
        this.name = name;
      },
      name: '',
      eat: function () {
        this.say('Yum!');
      },
      say: function (message) {
        console.log((this.name !== '' ? this.name + ': ' : this.name) + message);
      }
    });

    // Define the Cat class which extends Animal
    var Cat = Animal.extend({
      eat: function (food) {
        if (food instanceof Mouse) {
          this.base();
        } else {
          this.say('Yuk! I only eat mice.');
        }
      }
    });

    // Define a few more animals
    var Mouse = Animal.extend();
    var Dog = Animal.extend();

    // Try out the classes
    var kitty = new Cat('Kitty');
    kitty.eat(new Mouse()); // logs "Yum!"
    kitty.eat(new Dog()); // logs "Yuk! I only eat mice."

Notice the use of `this.base()`. `this.base()` is how you access the parent's method. This works in all methods (including constructors).

You can also define static (class-level) properties and methods:

    var Circle = Shape.extend({ // instance properties / methods
      constructor: function (x, y, radius) {
        this.base(x, y);
        this.radius = radius;
      },
      radius: 0,
      getCircumference: function () {
        return 2 * Circle.PI * this.radius;
      }
    }, { // class properties / methods
      PI: 3.14
    });

For more details including private data and singleton objects check out Dean Edward's [original documentation](http://dean.edwards.name/weblog/2006/03/base/).

# License

**The MIT License**

Based on Base.js 1.1a (c) 2006 - 2010 Dean Edwards
Updated to pass JSHint and converted into a Module format by Kenneth Powers

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
