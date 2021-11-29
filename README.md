# Example FBSnapshotTestCase with Snapshot and Texture
this repository contains an example app to include a reproduction of an issue with the Texture framework combined with FBSnapshotTestCase. 

Description of the issue: Integrating Texture Framework while using FBSnapshotTestCase Framework to run UI Tests, tests will fail showing diff failure between different UI elements. in the example below we will see one example of UI changing (this time - its round corners but not limited only to that). 

Below - Instructions on how to reproduce the failures using the example app from this repository:
1. Download the zip file "Example_app_with_texture_and_FBSnapshotTestCase.zip" from this repo (or clone this repo by using "git clone https://github.com/0xkuj/Example_APP_with_Snapshot_and_Texture.git"
2. Unzip the file and open "App.xcodeproj" (Note - I use Xcode 13.1 but it is probably not a must)

3. Make sure "AsyncDisplayKit.xcodeproj" is under "Core"


![Screen Shot 2021-11-29 at 14 49 45](https://user-images.githubusercontent.com/56236821/143871089-43f5f0a1-a9fb-4e66-b88f-662c176b1c17.png)

4. Make sure the "Core" Target is using "AsyncDisplayKit.framework" 


![Screen Shot 2021-11-29 at 14 51 16](https://user-images.githubusercontent.com/56236821/143871284-ae8f8e38-8315-4c3a-b525-9edcc0e48759.png)

5. Go to Test Navigator tab in Xcode
6. Make sure your simulator is on device running 14.0.1 (this should not be iOS specific, but this test case is working 100% of the times) (I am using iPhone 11 Pro with iOS 14.0.1) 
7. run the tests named "FeatureTests" - this stage will run the UI tests using the "Snapshot" framework. tests will must likely fail. in the diff file ("FailureDiffs") 


![Screen Shot 2021-11-29 at 14 55 39](https://user-images.githubusercontent.com/56236821/143871921-86bb1b5a-b099-436f-a04e-41a3758945de.png)

8. Check the failure diff inside the folder, and the diff will look like this:


![Screen Shot 2021-11-29 at 14 57 38](https://user-images.githubusercontent.com/56236821/143872171-7afb34b4-2487-4efb-95b2-f414d6aa1a92.png)

This actually means that the Snapshot framework is trying to compare between a screen it expects to find 


![testSnapshot@3x](https://user-images.githubusercontent.com/56236821/143872440-dca827ee-2220-4153-927c-eb461abc8c81.png)
vs what it actually finds (this is due to Texture framework integration - once the Texture framework is removed from within the "Core" frameworks list {stage 4} the issue is gone)


![failed_testSnapshot@3x](https://user-images.githubusercontent.com/56236821/143872584-a990e4ec-88fc-4aa6-82ee-aa44d5d73bf3.png)


Consider - Suggested solution:
We found that moving the initialization of allowsGroupOpacityFromUIKitOrNil and allowsEdgeAntialiasingFromUIKitOrNil from 
"ASInitializeFrameworkMainThread(void)" to their respective functions before being used (in this one and only time) (BOOL ASDefaultAllowsGroupOpacity() and BOOL ASDefaultAllowsEdgeAntialiasing()) will solve this issue.
![Screen Shot 2021-11-29 at 15 15 01](https://user-images.githubusercontent.com/56236821/143875343-d4aaced4-dc41-471e-87fd-699d76e1361d.png)
