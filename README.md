# Object Anchor SDK
Detects 3D objects using point clouds from ARCore depth images

**Note**: Requires Depth API support - [supported devices](https://developers.google.com/ar/devices)

This project shows a sample usage of the Object Anchor SDK with [ARCore - HelloAR Java](https://github.com/google-ar/arcore-android-sdk) 

## Steps to add Object Anchor SDK to existing project
- Add objectanchorsdk.aar to current project
- Create an ObjectAnchor object in activity and add below code
```
ObjectAnchor objectAnchor;
```
```
  objectAnchor = new ObjectAnchor(this, session, new ObjectAnchorEvents() {
      @Override
      public void onScenePointsUpdated(float[] points) {
        //Scanned points x,y,z,x,y,z... format
      }

      @Override
      public void onObjectPointsFound(float[] objectPoints) {
        //Aligned points x,y,z,x,y,z... format
      }

      @Override
      public void onObjectTransformationUpdated(float[] transformation) {
        //Transformation matrix4x4
        objectAnchor.StopScan();
      }
    });

    objectAnchor.inputTemplatePCD(this, R.raw.template);  //.pcd file ASCII format or can be input as List<float> x,y,z,x,y,z...

    objectAnchor.StartScan();
```
```
  @Override
  public void onPause() {
    super.onPause();
      if(objectAnchor != null)
        objectAnchor.StopScan();
  }
```
