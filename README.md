# JSResizeLargeImages

## Source code

```javascript
function resizeLargeImages() {
	imgArray = document.getElementsByTagName("img");
	for (var i = 0; i < imgArray.length; i++) {
		if (imgArray[i] == null) { continue; }
		var resizedCanvas = convertImageToCanvasAndResize(imgArray[i]);
		if (resizedCanvas != null) {
			// function convertCanvasToImage will throw error if canvas.toDataURL is not allowed
		//	var resizedImage = convertCanvasToImage(resizedCanvas);
		//	imgArray[i].parentNode.replaceChild(resizedImage, imgArray[i]);
			// image is replaced with resized canvas (recommended mode)
			imgArray[i].parentNode.replaceChild(resizedCanvas, imgArray[i]); 
		}
	}
}

 function convertImageToCanvasAndResize(image) {
 		var maxWidth = 500; // Max width for the canvas
        var maxHeight = 500;    // Max height for the canvas
        var ratio = 0.0;  // Used for aspect ratio
        var width = image.width;    // Current image width
        var height = image.height;  // Current image height

        // Check if the current width is larger than the max
        if(width > maxWidth) {
            ratio = maxWidth / width;   // get ratio for scaling image
        } else if(height > maxHeight) {
        		ratio = maxHeight / height; // get ratio for scaling image
        } else {
        		return; // image is smaller then maxWidth and maxHeight
        }
        
        height = height * ratio;    // Reset height to match scaled image
       	width = width * ratio;    // Reset width to match scaled image
		var canvas = document.createElement("canvas");
		canvas.width = width
		canvas.height = height
		canvas.getContext("2d").drawImage(image, 0, 0, width, height);
		return canvas;
 }
 
 function convertCanvasToImage(canvas) {
	var image = new Image();
	image.crossOrigin = "Anonymous";
	image.src = canvas.toDataURL("image/png");
	return image;
}

document.getElementsByTagName("body")[0].onload = resizeLargeImages;	// example usage
```
