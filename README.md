# Example FBSnapshotTestCase with Snapshot and Texture
this repository contains an example app to reproduce an issue with the Texture framework combined with FBSnapshotTestCase. this issue is causing UI test that are running via the snapshot framework to fail, for example, on round corners. removing Texture framework will resolve this issue

Instructions:
1. download the zip file "Example_app_with_texture_and_FBSnapshotTestCase.zip"
2. open "App.xcodeproj" (I use Xcode 13.1)
3. make sure "AsyncDisplayKit.xcodeproj" is under "Core" (image) 
4. Make sure the "Core" Target is using "AsyncDisplayKit.framework" (image)
5. Go to Test Navigator tab in Xcode (image)
6. Make sure your simulator is on device running 14.0.1 (this should not be iOS specific, but this test case is working 100% of the times) (I am using iPhone 11 Pro with iOS 14.0.1) (image)
7. run the tests named "FeatureTests" - this stage will run the UI tests using the "Snapshot" framework. tests will must likely fail. in the diff file ("FailureDiffs") (image)
