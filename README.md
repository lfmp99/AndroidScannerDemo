# ScanLibrary
ScanLibrary is an android document scanning library built on top of OpenCV, using the app you will be able to select the exact edges and crop the document accordingly from the selected 4 edges and change the perspective transformation of the cropped image.

# Screenshots

<div align="center">

		<img width="23%" src="https://raw.githubusercontent.com/jhansireddy/AndroidScannerDemo/master/ScanDemoExample/screenshots/scanInput.png" alt="Scan Input" title="Scan Input"</img>
        <img height="0" width="8px">
        <img width="23%" src="https://raw.githubusercontent.com/jhansireddy/AndroidScannerDemo/master/ScanDemoExample/screenshots/scanPoints.png" alt="Scan Points" title="Scan Input"</img>
        <img height="0" width="8px">
        <img width="23%"src="https://raw.githubusercontent.com/jhansireddy/AndroidScannerDemo/master/ScanDemoExample/screenshots/blackWhiteScannedResult.png" alt="After Scan" title="After Scan"></img>
        <img height="0" width="8px">
        <img width="23%" src="https://raw.githubusercontent.com/jhansireddy/AndroidScannerDemo/master/ScanDemoExample/screenshots/returned_scan_result.png" alt="Scanned Result" title="Scanned Result"></img>
</div>

# Videos


<div align="center" >
<a href="http://www.youtube.com/watch?feature=player_embedded&v=Kl7rRZ79m6k" target="_blank"><img src="https://raw.githubusercontent.com/jhansireddy/AndroidScannerDemo/master/ScanDemoExample/screenshots/scanPoints.png" 
alt="Scan Video" width="40%" border="10" /></a>
</div>


# Using it in your project
- If you are using android studio, add the dependency to your main app build.gradle this way: 
```	    
compile project(':scanlibrary')
```
- In your activity or fragment when you want to give an option of document scanning to user then:
Start the scanlibrary ScanActivity, with this the app will go to library, below is the sample code snippet:
Note: preference can be one of OPEN_CAMERA or OPEN_MEDIA or left empty, based on the passed preference the scan library decides to open camera or media or open the scan home page.
```java
       int REQUEST_CODE = 99;
       int preference = ScanConstants.OPEN_CAMERA;
       Intent intent = new Intent(this, ScanActivity.class);
       intent.putExtra(ScanConstants.OPEN_INTENT_PREFERENCE, preference);
       startActivityForResult(intent, REQUEST_CODE);
```

- Once the scanning is done, the application is returned from scan library to main app, to retrieve the scanned image, add onActivityResult in your activity or fragment from where you have started startActivityForResult, below is the sample code snippet:
```java
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (requestCode == REQUEST_CODE && resultCode == Activity.RESULT_OK) {
            Uri uri = data.getExtras().getParcelable(ScanConstants.SCANNED_RESULT);
            Bitmap bitmap = null;
            try {
                bitmap = MediaStore.Images.Media.getBitmap(getContentResolver(), uri);
                getContentResolver().delete(uri, null, null);
                scannedImageView.setImageBitmap(bitmap);
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
```
- ScanDemoWorkingEclips is a version for eclips. you just need to import it as Android Project and the project will run. the small changes i have done is the color for edge detection and on result_scan activity i have automatically calling Magic gray scale change method and i have put openCV-3..

- **IMPORTANT:** This project uses the OPENCV Framework. Download the newest version here 'http://opencv.org/.
