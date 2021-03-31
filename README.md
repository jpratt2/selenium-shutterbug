# seleniumCompareFullpageScreenshots version 1.1
This fork of [selenium-shutterbug](https://github.com/assertthat/selenium-shutterbug) (Java) offers 2 additional methods for full-page screenshot comparisons.  
It is used for site monitoring to check if anything has visually changed on a list of web pages. Best in Firefox, but also works in Chrome.

## Additional Methods

### `Shutterbug.compareScreenshotFP`  
Compares a web page against an expected image.  
If there is a difference between them (beyond the acceptance threshold), an image is generated with the difference marked in red. This image is a failure report and is called a "diff image". 

#### maximum options:  
`compareScreenshotFP(WebDriver driver, String expectedImageFolderPath, String expectedImageName, String diffImageFolderPath, String diffImageName, Double deviation)`

#### default options: 
`compareScreenshotFP(WebDriver driver)`

#### default values:
option | value 
------- |------ 
expectedImageFolderPath | a folder called "screenshots" at the project root
expectedImageName | based on the URL
diffImageFolderPath | a folder called "screenshots" at the project root  
diffImageName | based on the URL with "DIFF_IMAGE" appended. 
deviation| 0.0  No variation between the images is allowed.  

No diff image will be created if there is no difference.
The last parameter "deviation" is the acceptance threshold. For example, the value of 0.9 is a lenient acceptance threshold, allowing a difference of up to 90% before reporting a failure.

---
  
### `Shutterbug.screenshotFP`  
Makes a full-page screenshot of a web page.

#### maximum options: 
`screenshotFP(WebDriver driver, String folderPath, String fileName)`

#### default options:  
`screenshotFP(WebDriver driver)`  
#### default values: 
option | value 
------- |------ 
folderPath| a folder called "screenshots" at the project root  
fileName | based on the URL (in the same way as compareScreenshotFP)

---  
## Examples
1. Make a baseline screenshot for comparison and put it in a folder called "expected" at the project root (next to pom.xml if using Maven).
```
driver.get("https://yourdomain.com");
Shutterbug.screenshotFP(driver, "expected");
```

2. Compare that same URL against the baseline, which is now in a folder called "expected".  
If there is a diff image, put it in a folder called "observed".  
Please note, it is necessary to create the folder called "observed" first.  
```
driver.get("https://yourdomain.com");
Shutterbug.compareScreenshotFP(driver,"expected","observed");
```
---
## Usage
This is set up as a Maven project.
It is necessary to add a delay after visiting the page, for example:
```
driver.get("https://yourpage.com");
Thread.sleep(5000);
```
Otherwise, it may not work.



