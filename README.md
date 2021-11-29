# Example FBSnapshotTestCase with Snapshot and Texture
this repository contains an example app to reproduce an issue with the Texture framework combined with FBSnapshotTestCase. this issue is causing UI test that are running via the snapshot framework to fail, for example, on round corners. removing Texture framework will resolve this issue

Instructions on how to reproduce the failures:
1. download the zip file "Example_app_with_texture_and_FBSnapshotTestCase.zip" from this repo (or clone this repo by using "git clone https://github.com/0xkuj/Example_APP_with_Snapshot_and_Texture.git"
2. open "App.xcodeproj" (Note - I use Xcode 13.1 but it is probably not a must)
3. make sure "AsyncDisplayKit.xcodeproj" is under "Core" (image) ![Screen Shot 2021-11-29 at 14 49 45](https://user-images.githubusercontent.com/56236821/143871089-43f5f0a1-a9fb-4e66-b88f-662c176b1c17.png)
4. Make sure the "Core" Target is using "AsyncDisplayKit.framework" (image)
5. Go to Test Navigator tab in Xcode (image)
6. Make sure your simulator is on device running 14.0.1 (this should not be iOS specific, but this test case is working 100% of the times) (I am using iPhone 11 Pro with iOS 14.0.1) (image)
7. run the tests named "FeatureTests" - this stage will run the UI tests using the "Snapshot" framework. tests will must likely fail. in the diff file ("FailureDiffs") (image)
