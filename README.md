## jQuery Amelia
Amelia is a jQuery plugin for retrieving basic meta information from the files you upload.

### Dependencies
- jQuery

### Simple Usage
this example is basic. using a array which we consider to be native temporary storage.

```html
<button id="btn">Show</button>
<input type="file" id="myFile">
```

and the script section:

```js
var myNative = [];

$("#myFile").ameliaMetaImages({
    storage: myNative
});

$("#btn").on('click', function () {
    console.log(myNative);
});
```

After you clik button, in the console, you can see output like this:

```js
[
    {
        data: "iVBORw0KGgoAAAA...."
        raw : "data:image/png;base64iVBORw0KGgoAAAA...."
        size: 20079
        type: "image/png"
    }...
]
```

### Show Image File into Page
you can display the image file from the `row` meta data into the` src` attribute of the image element:

```html
<button id="btn">Show</button>
<div id="myDataImage"></div>
<input type="file" id="myFile">
```

```js
...

$("#btn").on('click', function () {
    // Clear data html
    $("#myDataImage").html("");
    
    $.each(myNative, function (index, value) {
        // Image element
        var myImage = $("<img style=\"width: 30%; margin: 5px; border: 2px solid gray;\">");
        myImage.attr("src", value.raw);
        
        $("#myDataImage").append(myImage);
    });
});
```

After you clik button, in the console, you can see output like this:

![](example/images/native.png?raw=true)


### Advanced Usage (KnockoutJS)
You can use it with KnockoutJS. It's easier and more fun because the storage we're using is really under observable from knockout.

```js
var VM = {
    data: {
        files: ko.observableArray([])
    },
    methods: {
        onRemoveFiles: function (data, event) { ... },
        onList: function () {
            console.log(VM.data.files());
        }
    }
};

ko.computed(function () {
    $("#myFile").ameliaMetaImages({
        storage: VM.data.files()
    });
});

ko.applyBindings([VM]);
```

### License
[MIT License](http://www.opensource.org/licenses/mit-license.php)
