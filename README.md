Patio
=====

Patio is a minimalistic Android view widget for selecting multiple images. 

[Demo Video](http://youtu.be/rg1SD7RO85o)

## Instructions

Patio can be added to an Activity or Fragment using the following XML

```XML
<com.andressantibanez.android.patio.Patio
  android:id="@+id/patio"
  android:layout_width="match_parent"
  android:layout_height="wrap_content"
  app:thumbnailHeight="200dp"
  app:thumbnailWidth="200dp"
  app:thumbnailsContainerPadding="10dp"
  app:thumbnailsContainerBackground="#ddd"
  app:maxPictures="3"
  app:thumbnailsMessage="@string/patio_footer"
  app:actionsTextColor="#333"/>
```

Patio has certain customizable attributes:
- ***thumbnailHeight*** defines the thumbnails height.
- ***thumbnailWidth*** defines the thumbnails width.
- ***thumbnailsContainerPadding*** defines how much padding will be used for the thumbnails container.
- ***thumbnailsContainerBackground*** defines a background color for the thumbnails container.
- ***maxPictures*** specifies how many pictures can the user add to the Patio view.
- ***thumbnailsMessage*** defines a custom string for the views footer. This string can be used with %1$d and %2$d tokens to add a pictures attached / max pictures message.
- ***actionsTextColor*** defines the text color for each action: Take Picture, Attach Picture, Remove Picture, Clear.

To add this attributes you must add the following definition to the root view
```XML
xmlns:app="http://schemas.android.com/apk/res-auto"
```

Make sure the Activity or Fragment implements PatioCallbacks. In this callbacks we will handle ***startActivityForResult*** intent for adding pictures via Camera or Gallery. You can get these intents from `getTakePictureIntent()` or `getAttachPictureIntent()`.

***Callbacks***
```java
@Override
public void onTakePictureClick() {
    Intent intent = mPatio.getTakePictureIntent();
    startActivityForResult(intent, REQUEST_CODE_TAKE_PICTURE);
}

@Override
public void onAddPictureClick() {
    Intent intent = mPatio.getAttachPictureIntent();
    startActivityForResult(intent, REQUEST_CODE_ATTACH_PICTURE);
}
```
Also, make sure you register you register your Activity or Fragment to get notified when callbacks are fired.

***Listener***
```java
mPatio = (Patio) findViewById(R.id.patio);
mPatio.setCallbacksListener(this);
```

Patio needs the following permissions in your app in order to work properly.
```XML
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-feature android:name="android.hardware.camera" />
```
To get an ArrayList of the pictures added to Patio you can call `getThumbnailsPaths()` method.
```java
ArrayList<String> thumbnails = mPatio.getThumbnailsPaths();
```

License
=======
Copyright 2014 Andrés Santibáñez

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
