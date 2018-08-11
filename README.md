# sharepoint-clientside-alphabetize-calendar-overlays
Alphabetize the calendar overlays on the left side bar.

## Alphabetize Calendar Overlays on a Microsoft SharePoint 2013 Calendar
The following is a client side JavaScript + jQuery script that can be used for alphabetizing the overlays instead of having to delete all of them and creating them in order.

```
var overlays = $('a.ms-acal-apanel-item');
delete overlays.length;
delete overlays.proto;
delete overlays.prevObject;

var arrOverlays = Object.keys(overlays).map(function(key) {
  return [overlays[key]];
});

var sortedOverlays = arrOverlays.sort(function(x, y){
	var text1 = x[0].text.toLowerCase();
	var text2 = y[0].text.toLowerCase();
	return text1 > text2;
});

var html = "<ul>";

for (var c = 0; c < sortedOverlays.length; c++ ) {
	html += "<li>" + sortedOverlays[c][0].outerHTML + "</li>";
}

html += "</ul>";

// The following selector may vary; use the browser's inspector to properly select the panel/side bar and copy the CSS selector
$('.ms-acal-apanel > ul:nth-child(1) > li:nth-child(1) > ul:nth-child(2)')[0].outerHTML = html;
```
