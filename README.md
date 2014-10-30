Patio
=====

Patio is a minimalistic Android view widget for selecting multiple images. It can be added to an Activity or Fragment using the following XML

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
Make sure the Activity or Fragment implements PatioCallbacks. In this callbacks we will handle ***startActivityForResult*** intent for adding pictures via Camera or Gallery. You can get these intents from getTakePictureIntent() or getAttachPictureIntent().

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
