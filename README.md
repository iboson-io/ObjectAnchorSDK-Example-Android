# Object Anchor SDK
Detects 3D objects from uploaded 3D models

**Note**: Requires ARCore support - [supported devices](https://developers.google.com/ar/devices)

This project shows a sample usage of the Object Anchor SDK with [ARCore - HelloAR Java](https://github.com/google-ar/arcore-android-sdk) 

## Steps to add Object Anchor SDK to existing project
- Add [objectanchorsdk.aar](https://github.com/iboson-io/ObjectAnchorSDK-ARCoreExample-Android/releases) to current project
- Create an ObjectAnchor object in activity and add below code
```
ObjectAnchor objectAnchor;
```
```
   objectAnchor = new ObjectAnchor(this, session, new ObjectAnchorEvents() {
      @Override
      public void onInitialized() {
        objectAnchor.setDetectionConfig("MODEL_ID", "TOKEN");
      }
      @Override
      public void onDetected(float[] transformation) {
        //Transformation matrix4x4
      }
      @Override
      public void onFailed(String error) {
        //Failure details
      }
    });

   scanButton?.setOnClickListener {
      objectAnchor?.StartScan()
     }

```
```
  @Override
  public void onPause() {
    super.onPause();
      if(objectAnchor != null)
        objectAnchor.StopScan();
  }
```
