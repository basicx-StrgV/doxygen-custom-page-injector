# doxygen-custom-page-injector
Inject custom html pages into your doxygen documentation, that can be navigated to and contain the header and footer layout.

## How to use

First download the `doxygen-custom-page-injector.js` script from this repository. 

### Configuring the layout
Use doxygen to create a custom layout xml file.  
The layout file can be created with the following command:
```
doxygen -l
```

After that open your doxyfile and add the layout file.
```
LAYOUT_FILE = DoxygenLayout.xml
```

Open your layout file and add an entry for your html file to the end of the `navindex`.
``` xml
<navindex>
  ...
  <tab type="user" url="sample.html" title="SamplePage"/>
</navindex>
```

For more information about the layout file, please check the [doxygen docs](https://www.doxygen.nl/manual/customize.html#layout).

### Adding the files to the doxyfile
To make the script and your html file available in the created doc they need to be added to the doxyfile as extra html files.

```
HTML_EXTRA_FILES       = sample.html \
                         js/doxygen-custom-page-injector.js
```

### Setting up the html file
For the injection to work, the html file needs to be set up in the right way.

``` html
<script type="text/javascript" src="./doxygen-custom-page-injector.js"></script>

<div id="injection-wrapper" nav-to="sample.html" style="display: none;">
    <!-- Your HTML goes here -->
</div>
```

The first thing in the html file should be the linked injection script.  

After that comes a `div` element that wraps the html that should be injected into the doxygen layout.  
This div needs to have the `id` `injection-wrapper` to allow the script to find it.  
The `nav-to` attribute should contain the name of your html file, so doxygen knows what navigation item to select.  

Setting the `display` style to `none` is optional but recommended if you don't want anything to show up before it gets injected.

**All of your custom html should be inside of the `injection-wrapper` element, because only the content of that element will be injected and the rest will be trimmed.**

*If there are any problems or you have some questions, feel free to open an [issue](https://github.com/basicx-StrgV/doxygen-custom-page-injector/issues).*
