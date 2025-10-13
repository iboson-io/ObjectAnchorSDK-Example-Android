# Object Anchor SDK
Detects 3D objects using point clouds from ARCore depth images

**Note**: Requires Depth API support - [supported devices](https://developers.google.com/ar/devices)

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
        objectAnchor.setDetectionConfig(ObjectAnchor.DetectionType.POINTCLOUD, "MODEL_ID", "TOKEN");
        objectAnchor.StartScan();
      }
      @Override
      public void onStatusUpdated(String status) {
        //Scan status
      }
      @Override
      public void onObjectTransformationUpdated(float[] transformation) {
        //Transformation matrix4x4
        objectAnchor.StopScan();
      }
    });

    objectAnchor.setConfidence(0.95f);
    objectAnchor.setMaxScanDistance(2.5f);
```
```
  @Override
  public void onPause() {
    super.onPause();
      if(objectAnchor != null)
        objectAnchor.StopScan();
  }
```
