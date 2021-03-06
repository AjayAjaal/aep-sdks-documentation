# Media API reference

## Media API reference

### createTracker

{% hint style="warning" %}
The API createTracker with callback has been deprecated for the synchronous version
{% endhint %}

Creates a media tracker instance that tracks the playback session. The tracker created should be used to track the streaming content, and it sends periodic pings to the media analytics backend.

{% tabs %}
{% tab title="Android" %}
#### createTracker

The createTracker function returns the instance of MediaTracker for tracking a media session. The createTracker function with callback as a parameter has been deprecated.

**Syntax**

```java
public static MediaTracker createTracker()

// Deprecated
public static void createTracker(AdobeCallback<MediaTracker> callback)
```

**Example**

```java
MediaTracker mediaTracker = Media.createTracker();  // Use the instance for tracking media.

// Deprecated
Media.createTracker(new AdobeCallback<MediaTracker>() {
    @Override
    public void call(MediaTracker mediaTracker) {
        // Use the instance for tracking media.
    }
});
```
{% endtab %}

{% tab title="iOS" %}
#### createTracker

The createTracker function returns the instance of ACPMediaTracker for tracking a media session. The createTracker function with callback as a parameter has been deprecated.

**Syntax**

```objectivec
+(ACPMediaTracker* _Nullable) createTracker;


// Deprecated
+(void) createTracker: (void (^ _Nonnull) (ACPMediaTracker* _Nullable)) callback;
```

**Examples**

Here are examples in Objective C and Swift:

**Objective C**

```objectivec
ACPMediaTracker *mediaTracker = [ACPMedia createTracker];  // Use the instance for tracking media.


// Deprecated
[ACPMedia createTracker:^(ACPMediaTracker * _Nullable mediaTracker) {
    // Use the instance for tracking media.
}];
```

**Swift**

```swift
let mediaTracker = ACPMedia.createTracker()  // Use the instance for tracking media.

// Deprecated
ACPMedia.createTracker({mediaTracker in
    // Use the instance for tracking media.
})
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

#### createTracker

```jsx
ACPMedia.createTracker().then(tracker =>
  this.setState({currentTracker: tracker})
);
```
{% endtab %}
{% endtabs %}

### createTrackerWithConfig

Creates a media tracker instance based on the configuration to track the playback session.

| Key | Description | Value | Required |
| :--- | :--- | :--- | :---: |
| `config.channel` | Channel name for media. Set this to overwrite the channel name configured from launch for media tracked with this tracker instance. | String | No |
| `config.downloadedcontent` | Creates a tracker instance to track downloaded media. Instead of sending periodic pings, the tracker only sends one ping for the entire content. | Boolean | No |

{% tabs %}
{% tab title="Android" %}
#### createTracker

Optional configuration about the tracker can be passed to this function. The createTracker function returns the instance of MediaTracker with the configuration for tracking a media session. The createTracker function with callback as a parameter has been deprecated.

**Syntax**

```java
public class MediaConstants {

    public static final class Config {
        public static final String CHANNEL = "config.channel";
        public static final String DOWNLOADED_CONTENT = "config.downloadedcontent";
    }

}

public static MediaTracker createTracker(Map<String, Object> config)

// Deprecated
public static void createTracker(Map<String, Object> config, final AdobeCallback<MediaTracker> callback)
```

**Example**

```java
HashMap<String, Object> config = new HashMap<String, Object>();
config.put(MediaConstants.Config.CHANNEL, "custom-channel");  // Override channel configured from launch
config.put(MediaConstants.Config.DOWNLOADED_CONTENT, true);   // Creates downloaded content tracker


MediaTracker mediaTracker = Media.createTracker(config);  // Use the instance for tracking media.

// Deprecated
Media.createTracker(config, new AdobeCallback<MediaTracker>() {
    @Override
    public void call(MediaTracker mediaTracker) {
        // Use the instance for tracking media.
    }
});
```
{% endtab %}

{% tab title="iOS" %}
#### createTrackerWithConfig

Optional configuration about the tracker can be passed to this function. The createTracker function returns the instance of ACPMediaTracker with the configuration for tracking a media session. The createTracker function with callback as a parameter has been deprecated.

**Syntax**

```objectivec
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaKeyConfigChannel;
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaKeyConfigDownloadedContent;

+ (ACPMediaTracker* _Nullable) createTrackerWithConfig: (NSDictionary* _Nullable) config;

// Deprecated
+ (void) createTrackerWithConfig: (NSDictionary* _Nullable) config
                        callback: (void (^ _Nonnull) (ACPMediaTracker* _Nullable)) callback;
```

**Examples**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
NSMutableDictionary* config = [NSMutableDictionary dictionary];
config[ACPMediaKeyConfigChannel] = @"custom-channel"; // Override channel configured from launch
config[ACPMediaKeyConfigDownloadedContent] = @YES;    // Creates downloaded content tracker

ACPMediaTracker *mediaTracker = [ACPMedia createTrackerWithConfig:config]; // Use the instance for tracking media.

// Deprecated
[ACPMedia createTrackerWithConfig: config
                         callback:^(ACPMediaTracker * _Nullable mediaTracker) {
    // Use the instance for tracking media.
}];
```

**Swift**

```swift
var config: [String: Any] = [:]
config[ACPMediaKeyConfigChannel] = "custom-channel"  // Override channel configured from launch
config[ACPMediaKeyConfigDownloadedContent] = true    // Creates downloaded content tracker

let mediaTracker = ACPMedia.createTrackerWithConfig(config); // Use the instance for tracking media.

// Deprecated
ACPMedia.createTrackerWithConfig(config, {mediaTracker in
    // Use the instance for tracking media.
}
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

#### createTracker

```jsx
var config = new Object();
config[ACPMediaConstants.ACPMediaKeyConfigChannel] = "customer-channel";  // Override channel configured from launch
config[ACPMediaConstants.ACPMediaKeyConfigDownloadedContent] = true;  // Creates downloaded content tracker
ACPMedia.createTrackerWithConfig(config).then(tracker =>
  this.setState({currentTracker: tracker})
);
```
{% endtab %}
{% endtabs %}

### createMediaObject

Creates an instance of the Media object.

| Variable Name | Description | Required |
| :--- | :--- | :---: |
| `name` | Media name | Yes |
| `mediaId` | Media unique identifier | Yes |
| `length` | Media length | Yes |
| `streamType` | [Stream type](media-api-reference.md#stream-type) | Yes |
| `mediaType` | [Media type](media-api-reference.md#media-type) | Yes |

{% tabs %}
{% tab title="Android" %}
#### createMediaObject

Returns a HashMap instance that contains information about the media.

**Syntax**

```java
public static HashMap<String, Object> createMediaObject(String name,
                                                        String mediaId,
                                                        Double length,
                                                        String streamType,
                                                        MediaType mediaType);
```

**Example**

```java
HashMap<String, Object> mediaInfo = Media.createMediaObject("video-name",
                                                            "video-id",
                                                            60D,
                                                            MediaConstants.StreamType.VOD,
                                                            Media.MediaType.Video);
```
{% endtab %}

{% tab title="iOS" %}
#### createMediaObjectWithName

Returns an NSDictionary instance that contains information about the media.

**Syntax**

```objectivec
+ (NSDictionary* _Nonnull) createMediaObjectWithName: (NSString* _Nonnull) name
                                             mediaId: (NSString* _Nonnull) mediaId
                                              length: (double) length
                                          streamType: (NSString* _Nonnull) streamType
                                           mediaType: (ACPMediaType) mediaType;
```

**Example**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
NSDictionary *mediaObject = [ACPMedia createMediaObjectWithName: @"video-name"
                                                        mediaId: @"video-id"
                                                         length: 60
                                                     streamType: ACPMediaStreamTypeVod
                                                      mediaType: ACPMediaTypeVideo];
```

**Swift**

```swift
let mediaObject = ACPMedia.createMediaObject(withName: "video-name", mediaId: "video-id",
                                               length: Double(60),
                                           streamType: ACPMediaStreamTypeVod,
                                            mediaType:ACPMediaType.video)
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

#### createMediaObject

```jsx
let mediaObject = ACPMedia.createMediaObject("video-name", "video-id", 60, ACPMediaConstants.ACPMediaStreamTypeVod, ACPMediaType.Video);
```
{% endtab %}
{% endtabs %}

### createAdBreakObject

Creates an instance of the AdBreak object.

| Variable Name | Description | Required |
| :--- | :--- | :---: |
| `name` | Ad break name such as pre-roll, mid-roll, and post-roll. | Yes |
| `position` | The number position of the ad break within the content, starting with 1. | Yes |
| `startTime` | Playhead value at the start of the ad break. | Yes |

{% tabs %}
{% tab title="Android" %}
#### createAdBreakObject

Returns a HashMap instance that contains information about the ad break.

**Syntax**

```java
public static HashMap<String, Object> createAdBreakObject(String name, Long position, Double startTime);
```

**Example**

```java
HashMap<String, Object> adBreakObject = Media.createAdBreakObject("adbreak-name", 1L, 0D);
```
{% endtab %}

{% tab title="iOS" %}
#### createAdBreakObjectWithName

Returns an NSDictionary instance that contains information about the ad break.

**Syntax**

```objectivec
+ (NSDictionary* _Nonnull) createAdBreakObjectWithName: (NSString* _Nonnull) name
                                              position: (double) position
                                             startTime: (double) startTime;
```

**Example**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
NSDictionary *adBreakObject = [ACPMedia createAdBreakObjectWithName: @"adbreak-name"
                                                           position: 1
                                                          startTime: 0];
```

**Swift**

```swift
let adBreakObject = ACPMedia.createAdBreakObject(withName: "adbreak-name", position: 1, startTime: 0)
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

#### createAdBreakObject

```jsx
let adBreakObject = ACPMedia.createAdBreakObject("adbreak-name", 1, 0);
```
{% endtab %}
{% endtabs %}

### createAdObject

Creates an instance of the Ad object.

| Variable Name | Description | Required |
| :--- | :--- | :---: |
| `name` | Friendly name of the ad. | Yes |
| `adId` | Unique identifier for the ad. | Yes |
| `position` | The number position of the ad within the ad break, starting with 1. | Yes |
| `length` | Ad length | Yes |

{% tabs %}
{% tab title="Android" %}
#### createAdObject

Returns a HashMap instance that contains information about the ad.

**Syntax**

```java
public static HashMap<String, Object> createAdObject(String name, String adId, Long position, Double length);
```

**Example**

```java
HashMap<String, Object> adInfo = Media.createAdObject("ad-name", "ad-id", 1L, 15D);
```
{% endtab %}

{% tab title="iOS" %}
#### createAdObjectWithName

Returns an NSDictionary instance that contains information about the ad.

**Syntax**

```objectivec
+ (NSDictionary* _Nonnull) createAdObjectWithName: (NSString* _Nonnull) name
                                             adId: (NSString* _Nonnull) adId
                                         position: (double) position
                                           length: (double) length;
```

**Example**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
NSDictionary *adObject = [ACPMedia createAdObjectWithName: @"ad-name"
                                                     adId: @"ad-id"
                                                 position: 1
                                                   length: 15];
```

**Swift**

```swift
let adObject = ACPMedia.createAdObject(withName: "ad-name", adId: "ad-id", position: 1, length: 15)
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

#### createAdObject

```jsx
let adObject = ACPMedia.createAdObject("ad-name", "ad-id", 1, 15);
```
{% endtab %}
{% endtabs %}

### createChapterObject

Creates an instance of the Chapter object.

| Variable Name | Description | Required |
| :--- | :--- | :---: |
| `name` | Chapter name | Yes |
| `position` | The number position of the chapter within the content, starting with 1. | Yes |
| `length` | Chapter length | Yes |
| `startTime` | Playhead value at the start of the chapter | Yes |

{% tabs %}
{% tab title="Android" %}
#### createChapterObject

Returns a HashMap instance that contains information about the chapter.

**Syntax**

```java
public static HashMap<String, Object> createChapterObject(String name,
                                                          Long position,
                                                          Double length,
                                                          Double startTime);
```

**Example**

```java
HashMap<String, Object> chapterInfo = Media.createChapterObject("chapter-name", 1L, 60D, 0D);
```
{% endtab %}

{% tab title="iOS" %}
#### createChapterObjectWithName

Returns an NSDictionary instance that contains information about the chapter.

**Syntax**

```objectivec
+ (NSDictionary* _Nonnull) createChapterObjectWithName: (NSString* _Nonnull) name
                                              position: (double) position
                                                length: (double) length
                                             startTime: (double) startTime;
```

**Example**

Here are examples in Objective C and Swift:

**Objective C**

```objectivec
NSDictionary *chapterObject = [ACPMedia createChapterObjectWithName: @"chapter-name"
                                                           position: 1
                                                             length: 60
                                                          startTime: 0];
```

**Swift**

```swift
let chapterObject = ACPMedia.createChapterObject(withName: "chapter-name", position: 1, length: 60, startTime: 0)
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

#### createChapterObject

```jsx
let chapterObject = ACPMedia.createChapterObject('chapter-name', 1, 60, 0);
```
{% endtab %}
{% endtabs %}

### createQoEObject

Creates an instance of the QoE object.

| Variable Name | Description | Required |
| :--- | :--- | :---: |
| `bitrate` | Current bitrate | Yes |
| `startupTime` | Startup time | Yes |
| `fps` | FPS value | Yes |
| `droppedFrames` | Number of dropped frames | Yes |

{% hint style="info" %}
All the QoE values `bitrate`, `startupTime`, `fps`, `droppedFrames` would be converted to `long` for reporting purposes.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
#### createQoEObject

Returns a HashMap instance that contains information about the quality of experience.

**Syntax**

```java
public static HashMap<String, Object> createQoEObject(Long bitrate,
                                                      Double startupTime,
                                                      Double fps,
                                                      Long droppedFrames);
```

**Example**

```java
HashMap<String, Object> qoeInfo = Media.createQoEObject(10000000L, 2D, 23D, 10D);
```
{% endtab %}

{% tab title="iOS" %}
#### createQoEObjectWithBitrate

Returns an NSDictionary instance that contains information about the quality of experience.

**Syntax**

```objectivec
+ (NSDictionary* _Nonnull) createQoEObjectWithBitrate: (double) bitrate
                                          startupTime: (double) startupTime
                                                  fps: (double) fps
                                        droppedFrames: (double) droppedFrames;
```

**Example**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
NSDictionary *qoeObject = [ACPMedia createQoEObjectWithBitrate: 10000000
                                                   startupTime: 2
                                                           fps: 23
                                                 droppedFrames: 10];
```

**Swift**

```swift
let qoeObject = ACPMedia.createQoEObject(withBitrate: 10000000, startupTime: 2, fps: 23, droppedFrames: 10)
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

#### createQoEObject

```jsx
let qoeObject = ACPMedia.createQoEObject(1000000, 2, 23, 10);
```
{% endtab %}
{% endtabs %}

### createStateObject

Creates an instance of the Player State object.

| Variable Name | Description | Required |
| :--- | :--- | :---: |
| `name` | State name\(Use [Player State constants](media-api-reference.md#player-state-constants) to track standard player states\) | Yes |

{% tabs %}
{% tab title="Android" %}
#### createStateObject

Returns a HashMap instance that contains information about the State.

**Syntax**

```java
public static HashMap<String, Object> createStateObject(String stateName);
```

**Example**

```java
HashMap<String, Object> playerStateInfo = Media.createStateObject("fullscreen");
```
{% endtab %}

{% tab title="iOS" %}
#### createStateObjectWithName

Returns an NSDictionary instance that contains information about the player state.

**Syntax**

```objectivec
+ (NSDictionary* _Nonnull) createStateObjectWithName: (NSString* _Nonnull) stateName;
```

**Example**

Here are examples in Objective C and Swift:

**Objective C**

```objectivec
NSDictionary *playerStateObject = [ACPMedia createStateObjectWithName: @"fullscreen"];
```

**Swift**

```swift
let playerStateObject = ACPMedia.createStateObject(withName: "fullscreen")
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

#### createStateObject

```jsx
let playerStateObject = ACPMedia.createStateObject("fullscreen");
```
{% endtab %}
{% endtabs %}

## Media tracker API reference

### trackSessionStart

Tracks the intention to start playback. This starts a tracking session on the media tracker instance. For more information, see [Media Resume](media-api-reference.md#media-resume).

| Variable Name | Description | Required |
| :--- | :--- | :---: |
| `mediaInfo` | Media information created using the [createMediaObject](media-api-reference.md#createmediaobject) method. | Yes |
| `contextData` | Optional Media context data. For standard metadata keys, use [standard video constants](media-api-reference.md#standard-video-constants) or [standard audio constants](media-api-reference.md#standard-audio-constants). | No |

{% tabs %}
{% tab title="Android" %}
#### trackSessionStart

**Syntax**

```java
public void trackSessionStart(Map<String, Object> mediaInfo, Map<String, String> contextData);
```

**Example**

```java
HashMap<String, Object> mediaObject = Media.createMediaObject("media-name", "media-id", 60D, MediaConstants.StreamType.VOD, Media.MediaType.Video);

HashMap<String, String> mediaMetadata = new HashMap<String, String>();
// Standard metadata keys provided by adobe.
mediaMetadata.put(MediaConstants.VideoMetadataKeys.EPISODE, "Sample Episode");
mediaMetadata.put(MediaConstants.VideoMetadataKeys.SHOW, "Sample Show");

// Custom metadata keys
mediaMetadata.put("isUserLoggedIn", "false");
mediaMetadata.put("tvStation", "Sample TV Station");

_tracker.trackSessionStart(mediaInfo, mediaMetadata);
```
{% endtab %}

{% tab title="iOS" %}
#### trackSessionStart

**Syntax**

```objectivec
- (void) trackSessionStart: (NSDictionary* _Nonnull) mediaInfo data: (NSDictionary* _Nullable) contextData;
```

**Example**

Here are examples in Objective C and Swift:

**Objective C**

```objectivec
NSDictionary *mediaObject = [ACPMedia createMediaObjectWithName:@"media-name" mediaId:@"media-id" length:60 streamType:ACPMediaStreamTypeVod mediaType:ACPMediaTypeVideo];

NSMutableDictionary *mediaMetadata = [[NSMutableDictionary alloc] init];
// Standard metadata keys provided by adobe.
[mediaMetadata setObject:@"Sample show" forKey:ACPVideoMetadataKeyShow];
[mediaMetadata setObject:@"Sample season" forKey:ACPVideoMetadataKeySeason];

// Custom metadata keys
[mediaMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
[mediaMetadata setObject:@"Sample TV station" forKey:@"tvStation"];

[_tracker trackSessionStart:mediaObject data:mediaMetadata];
```

**Swift**

```swift
let mediaObject = ACPMedia.createMediaObject(withName: "media-name", mediaId: "media-id", length: 60, streamType: ACPMediaStreamTypeVod, mediaType:ACPMediaType.video)

// Standard metadata keys provided by adobe.      
var mediaMetadata = [ACPVideoMetadataKeyShow: "Sample show", ACPVideoMetadataKeySeason: "Sample season"]

// Custom metadata keys      
mediaMetadata["isUserLoggedIn"] = "false"
mediaMetadata["tvStation"] = "Sample TV station"

_tracker.trackSessionStart(mediaObject, data: mediaMetadata)
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

#### trackSessionStart

```jsx
let mediaObject = ACPMedia.createMediaObject("media-name", "media-id", 60, ACPMediaConstants.ACPMediaStreamTypeVod, ACPMediaType.Video);
var mediaMetadata = new Object();
mediaMetadata[ACPMediaConstants.ACPVideoMetadataKeyShow] = "Sample Show";
mediaMetadata[ACPMediaConstants.ACPVideoMetadataKeySeason] = "Sample Season";

// Custom metadata keys
mediaMetadata["isUserLoggedIn"] = "false";
mediaMetadata["tvStation"] = "Sample TV station";

tracker.trackSessionStart(mediaObject, mediaMetadata);
```
{% endtab %}
{% endtabs %}

### trackPlay

Tracks the media play, or resume, after a previous pause.

{% tabs %}
{% tab title="Android" %}
#### trackPlay

**Syntax**

```java
public void trackPlay();
```

**Example**

```java
_tracker.trackPlay();
```
{% endtab %}

{% tab title="iOS" %}
#### trackPlay

**Syntax**

```objectivec
- (void) trackPlay;
```

**Example**

Here are examples in Objective C and Swift:

**Objective C**

```objectivec
[_tracker trackPlay];
```

**Swift**

```swift
_tracker.trackPlay()
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

#### trackPlay

```jsx
tracker.trackPlay();
```
{% endtab %}
{% endtabs %}

### trackPause

Tracks the media pause.

{% tabs %}
{% tab title="Android" %}
#### trackPause

**Syntax**

```java
public void trackPause();
```

**Example**

```java
_tracker.trackPause();
```
{% endtab %}

{% tab title="iOS" %}
#### trackPause

**Syntax**

```objectivec
- (void) trackPause;
```

**Example**

Here are examples in Objective C and Swift:

**Objective C**

```objectivec
[_tracker trackPause];
```

**Swift**

```swift
_tracker.trackPause()
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

#### trackPause

```jsx
tracker.trackPause();
```
{% endtab %}
{% endtabs %}

### trackComplete

Tracks media complete. Call this method only when the media has been completely viewed.

{% tabs %}
{% tab title="Android" %}
#### trackComplete

**Syntax**

```java
public void trackComplete();
```

**Example**

```java
_tracker.trackComplete();
```
{% endtab %}

{% tab title="iOS" %}
#### trackComplete

**Syntax**

```objectivec
- (void) trackComplete;
```

**Example**

Here are examples in Objective C and Swift:

**Objective C**

```objectivec
[_tracker trackComplete];
```

**Swift**

```swift
_tracker.trackComplete()
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

#### trackComplete

```jsx
tracker.trackComplete();
```
{% endtab %}
{% endtabs %}

### trackSessionEnd

Tracks the end of a viewing session. Call this method even if the user does not view the media to completion.

{% tabs %}
{% tab title="Android" %}
#### trackSessionEnd

**Syntax**

```java
public void trackSessionEnd();
```

**Example**

```java
_tracker.trackSessionEnd();
```
{% endtab %}

{% tab title="iOS" %}
#### trackSessionEnd

**Syntax**

```objectivec
- (void) trackSessionEnd;
```

**Example**

Here are examples in Objective C and Swift:

**Objective C**

```objectivec
[_tracker trackSessionEnd];
```

**Swift**

```swift
_tracker.trackSessionEnd()
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

#### trackSessionEnd

```jsx
tracker.trackSessionEnd();
```
{% endtab %}
{% endtabs %}

### trackError

Tracks an error in media playback.

| Variable Name | Description | Required |
| :--- | :--- | :---: |
| `errorId` | Error Information | Yes |

{% tabs %}
{% tab title="Android" %}
#### trackError

**Syntax**

```java
public void trackError(String errorId);
```

**Example**

```java
_tracker.trackError("errorId");
```
{% endtab %}

{% tab title="iOS" %}
#### trackError

**Syntax**

```objectivec
- (void) trackError: (NSString* _Nonnull) errorId;
```

**Example**

Here are examples in Objective C and Swift:

**Objective C**

```objectivec
[_tracker trackError:@"errorId"];
```

**Swift**

```swift
_tracker.trackError("errorId")
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

#### trackError

```jsx
tracker.trackError("errorId");
```
{% endtab %}
{% endtabs %}

### trackEvent

Tracks media events.

| Variable Name | Description |
| :--- | :--- |
| `event` | [Media event](media-api-reference.md#media-events) |
| `info` | For an `AdBreakStart` event, the `adBreak` information is created by using the [createAdBreakObject](media-api-reference.md#createadbreakobject) method.   For an `AdStart` event, the Ad information is created by using the [createAdObject](media-api-reference.md#createadobject) method.   For `ChapterStart` event, the Chapter information is created by using the [createChapterObject](media-api-reference.md#createchapterobject) method.  For `StateStart` and `StateEnd` event, the State information is created by using the [createStateObject](media-api-reference.md#createstateobject) method. |
| `data` | Optional context data can be provided for `AdStart` and `ChapterStart` events. This is not required for other events. |

{% tabs %}
{% tab title="Android" %}
#### trackEvent

**Syntax**

```java
  public void trackEvent(Media.Event event,
                         Map<String, Object> info,
                         Map<String, String> data);
```

**Examples**

**Tracking Player States**

```java
// StateStart
  HashMap<String, Object> stateObject = Media.createStateObject("fullscreen");
  _tracker.trackEvent(Media.Event.StateStart, stateObject, null);

// StateEnd
  HashMap<String, Object> stateObject = Media.createStateObject("fullscreen");
  _tracker.trackEvent(Media.Event.StateEnd, stateObject, null);
```

**Tracking AdBreaks**

```java
// AdBreakStart
  HashMap<String, Object> adBreakObject = Media.createAdBreakObject("adbreak-name", 1L, 0D);
  _tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null);

// AdBreakComplete
  _tracker.trackEvent(Media.Event.AdBreakComplete, null, null);
```

**Tracking ads**

```java
// AdStart
  HashMap<String, Object> adObject = Media.createAdObject("ad-name", "ad-id", 1L, 15D);

  HashMap<String, String> adMetadata = new HashMap<String, String>();
  // Standard metadata keys provided by adobe.
  adMetadata.put(MediaConstants.AdMetadataKeys.ADVERTISER, "Sample Advertiser");
  adMetadata.put(MediaConstants.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign");
  // Custom metadata keys
  adMetadata.put("affiliate", "Sample affiliate");

  _tracker.trackEvent(Media.Event.AdStart, adObject, adMetadata);

// AdComplete
  _tracker.trackEvent(Media.Event.AdComplete, null, null);

// AdSkip
  _tracker.trackEvent(Media.Event.AdSkip, null, null);
```

**Tracking chapters**

```java
// ChapterStart
  HashMap<String, Object> chapterObject = Media.createChapterObject("chapter-name", 1L, 60D, 0D);

  HashMap<String, String> chapterMetadata = new HashMap<String, String>();
  chapterMetadata.put("segmentType", "Sample segment type");

  _tracker.trackEvent(Media.Event.ChapterStart, chapterDataInfo, chapterMetadata);

// ChapterComplete
  _tracker.trackEvent(Media.Event.ChapterComplete, null, null);

// ChapterSkip
  _tracker.trackEvent(Media.Event.ChapterSkip, null, null);
```

**Tracking playback events**

```java
// BufferStart
  _tracker.trackEvent(Media.Event.BufferStart, null, null);

// BufferComplete
  _tracker.trackEvent(Media.Event.BufferComplete, null, null);

// SeekStart
  _tracker.trackEvent(Media.Event.SeekStart, null, null);

// SeekComplete
  _tracker.trackEvent(Media.Event.SeekComplete, null, null);
```

**Tracking bitrate changes**

```java
// If the new bitrate value is available provide it to the tracker.
  HashMap<String, Object> qoeObject = Media.createQoEObject(2000000L, 2D, 25D, 10D);
  _tracker.updateQoEObject(qoeObject);

// Bitrate change
  _tracker.trackEvent(Media.Event.BitrateChange, null, null);
```
{% endtab %}

{% tab title="iOS" %}
#### trackEvent

**Syntax**

```objectivec
  - (void) trackEvent: (ACPMediaEvent) event
                 info: (NSDictionary* _Nullable) info
                 data: (NSDictionary* _Nullable) data;
```

**Examples**

**Tracking Player States**

Here are examples in Objective C and Swift:

**Objective C**

```objectivec
// StateStart
  NSDictionary* stateObject = [ACPMedia createStateObjectWithName:@"fullscreen"];
  [_tracker trackEvent:ACPMediaEventStateStart mediaObject:stateObject data:nil];

// StateEnd
  NSDictionary* stateObject = [ACPMedia createStateObjectWithName:@"fullscreen"];
  [_tracker trackEvent:ACPMediaEventStateEnd mediaObject:stateObject data:nil];
```

**Swift**

```swift
// StateStart
  let stateObject = ACPMedia.createStateObject(withName: "fullscreen")
  _tracker.trackEvent(ACPMediaEvent.stateStart, mediaObject: stateObject, data: nil)

// StateEnd
  let stateObject = ACPMedia.createStateObject(withName: "fullscreen")
  _tracker.trackEvent(ACPMediaEvent.stateEnd, mediaObject: stateObject, data: nil)
```

**Tracking AdBreaks**

Here are examples in Objective C and Swift:

**Objective C**

```objectivec
// AdBreakStart
  NSDictionary* adBreakObject = [ACPMedia createAdBreakObjectWithName:@"adbreak-name" position:1 startTime:0];
  [_tracker trackEvent:ACPMediaEventAdBreakStart mediaObject:adBreakObject data:nil];

// AdBreakComplete
  [_tracker trackEvent:ACPMediaEventAdBreakComplete mediaObject:nil data:nil];
```

**Swift**

```swift
// AdBreakStart
  let adBreakObject = ACPMedia.createAdBreakObject(withName: "adbreak-name", position: 1, startTime: 0)
  _tracker.trackEvent(ACPMediaEvent.adBreakStart, mediaObject: adBreakObject, data: nil)

// AdBreakComplete
  _tracker.trackEvent(ACPMediaEvent.adBreakComplete, mediaObject: nil, data: nil)
```

**Tracking Ads**

Here are examples in Objective C and Swift:

**Objective C**

```objectivec
// AdStart
  NSDictionary* adObject = [ACPMedia createAdObjectWithName:@"ad-name" adId:@"ad-id" position:1 length:15];
  NSMutableDictionary* adMetadata = [[NSMutableDictionary alloc] init];

  // Standard metadata keys provided by adobe.
  [adMetadata setObject:@"Sample Advertiser" forKey:ACPAdMetadataKeyAdvertiser];
  [adMetadata setObject:@"Sample Campaign" forKey:ACPAdMetadataKeyCampaignId];
  // Custom metadata keys
  [adMetadata setObject:@"Sample affiliate" forKey:@"affiliate"];

  [_tracker trackEvent:ACPMediaEventAdStart mediaObject:adObject data:adMetadata];

// AdComplete
  [_tracker trackEvent:ACPMediaEventAdComplete mediaObject:nil data:nil];

// AdSkip
  [_tracker trackEvent:ACPMediaEventAdSkip mediaObject:nil data:nil];
```

**Swift**

```swift
// AdStart
  let adObject = ACPMedia.createAdObject(withName: "ad-name", adId: "ad-id", position: 1, length: 15)

  // Standard metadata keys provided by adobe.
  var adMetadata = [ACPAdMetadataKeyAdvertiser: "Sample Advertiser", ACPAdMetadataKeyCampaignId: "Sample Campaign"]
  // Custom metadata keys
  adMetadata["affiliate"] = "Sample affiliate"

  _tracker.trackEvent(ACPMediaEvent.adStart, mediaObject: adObject, data: adMetadata)

// AdComplete
  _tracker.trackEvent(ACPMediaEvent.adComplete, mediaObject: nil, data: nil)

// AdSkip
  _tracker.trackEvent(ACPMediaEvent.adSkip, mediaObject: nil, data: nil)
```

**Tracking Chapters**

Here are examples in Objective C and Swift:

**Objective C**

```objectivec
// ChapterStart
  NSDictionary* chapterObject = [ACPMedia createChapterObjectWithName:@"chapter-name" position:1 length:30 startTime:0];

  NSMutableDictionary *chapterMetadata = [[NSMutableDictionary alloc] init];
  [chapterMetadata setObject:@"Sample segment type" forKey:@"segmentType"];

  [_tracker trackEvent:ACPMediaEventChapterStart mediaObject:chapterObject data:chapterMetadata];

// ChapterComplete
  [_tracker trackEvent:ACPMediaEventChapterComplete mediaObject:nil    data:nil];

// ChapterSkip
  [_tracker trackEvent:ACPMediaEventChapterSkip mediaObject:nil    data:nil];
```

**Swift**

```swift
// ChapterStart
  let chapterObject = ACPMedia.createChapterObject(withName: "chapter-name", position: 1, length: 60, startTime: 0)
  let chapterMetadata = ["Sample segment type": "segmentType"];

  _tracker.trackEvent(ACPMediaEvent.chapterStart, mediaObject: chapterObject, data: chapterMetadata)

// ChapterComplete
  _tracker.trackEvent(ACPMediaEvent.chapterComplete, mediaObject: nil, data: nil)

// ChapterSkip
  _tracker.trackEvent(ACPMediaEvent.chapterSkip, mediaObject: nil, data: nil)
```

**Tracking Playback events**

Here are examples in Objective C and Swift:

**Objective C**

```objectivec
// BufferStart
  [_tracker trackEvent:ACPMediaEventBufferStart info:nil data:nil];

// BufferComplete
  [_tracker trackEvent:ACPMediaEventBufferComplete info:nil data:nil];

// SeekStart
  [_tracker trackEvent:ACPMediaEventSeekStart info:nil data:nil];

// SeekComplete
  [_tracker trackEvent:ACPMediaEventSeekComplete info:nil data:nil];
```

**Swift**

```swift
// BufferStart
  _tracker.trackEvent(ACPMediaEvent.bufferStart, mediaObject: nil, data: nil)

// BufferComplete
  _tracker.trackEvent(ACPMediaEvent.bufferComplete, mediaObject: nil, data: nil)

// SeekStart
  _tracker.trackEvent(ACPMediaEvent.seekStart, mediaObject: nil, data: nil)

// SeekComplete
  _tracker.trackEvent(ACPMediaEvent.seekComplete, mediaObject: nil, data: nil)
```

**Tracking Bitrate change**

Here are examples in Objective C and Swift:

**Objective C**

```objectivec
// If the new bitrate value is available provide it to the tracker.
  NSDictionary* qoeObject = [ACPMedia createQoEObjectWithBitrate:2000000 startupTime:2 fps:25 droppedFrames:10];
  [_tracker updateQoEObject:qoeObject];

// Bitrate change
  [_tracker trackEvent:ACPMediaEventBitrateChange info:nil data:nil];
```

**Swift**

```swift
// If the new bitrate value is available provide it to the tracker.
  let qoeObject = ACPMedia.createQoEObject(withBitrate: 2000000, startupTime: 2, fps: 25, droppedFrames: 10)
  _tracker.updateQoEObject(qoeObject)

// Bitrate change
  _tracker.trackEvent(ACPMediaEvent.bitrateChange, mediaObject: nil, data: nil)
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

#### trackEvent

**Examples**

**Tracking Player States**

```jsx
// StateStart
  let stateObject = ACPMedia.createStateObject("fullscreen");
  tracker.trackEvent(ACPMediaEvent.EventStateStart, stateObject, null);

// StateEnd
  let stateObject = ACPMedia.createStateObject("fullscreen");
  tracker.trackEvent(ACPMediaEvent.EventStateEnd, stateObject, null);
```

**Tracking AdBreaks**

```jsx
// AdBreakStart
  let adBreakObject = ACPMedia.createAdBreakObject("adbreak-name", 1, 0);
  tracker.trackEvent(ACPMediaEvent.EventAdBreakStart, adBreakObject, null);

// AdBreakComplete
  tracker.trackEvent(ACPMediaEvent.EventAdBreakComplete, null, null);
```

**Tracking ads**

```jsx
// AdStart
  let adObject = ACPMedia.createAdObject("ad-name", "ad-id", 1, 15);
  var adMetadata = new Object();
  adMetadata[ACPMediaConstants.ACPAdMetadataKeyAdvertiser] = "Sample Advertiser";
  adMetadata[ACPMediaConstants.ACPAdMetadataKeyCampaignId] = "Sample Campaign";

  // Custom metadata keys
  adMetadata["affiliate"] = "Sample affiliate";

  tracker.trackEvent(ACPMediaEvent.EventAdStart, adObject, adMetadata);

// AdComplete
  tracker.trackEvent(ACPMediaEvent.EventAdComplete, null, null);

// AdSkip
  tracker.trackEvent(ACPMediaEvent.EventAdSkip, null, null);
```

**Tracking chapters**

```jsx
// ChapterStart
  let chapterObject = ACPMedia.createChapterObject("chapter-name", 1, 60, 0);
  var chapterMetadata = new Object();
  chapterMetadata["segmentType"] = "Sample segment type";

  tracker.trackEvent(ACPMediaEvent.EventChapterStart, chapterObject, chapterMetadata);

// ChapterComplete
  tracker.trackEvent(ACPMediaEvent.EventChapterComplete, null, null);

// ChapterSkip
  tracker.trackEvent(ACPMediaEvent.EventChapterSkip, null, null);
```

**Tracking playback events**

```jsx
// BufferStart
  tracker.trackEvent(ACPMediaEvent.EventBufferStart, null, null);

// BufferComplete
  tracker.trackEvent(ACPMediaEvent.EventBufferComplete, null, null);

// SeekStart
  tracker.trackEvent(ACPMediaEvent.EventSeekStart, null, null);

// SeekComplete
  tracker.trackEvent(ACPMediaEvent.EventSeekComplete, null, null);
```

**Tracking bitrate changes**

```jsx
// If the new bitrate value is available provide it to the tracker.
  let qoeObject = ACPMedia.createQoEObject(2000000, 2, 25, 10);
  tracker.updateQoEObject(qoeObject);

// Bitrate change
  tracker.trackEvent(ACPMediaEvent.EventBitrateChange, null, null);
```
{% endtab %}
{% endtabs %}

### updateCurrentPlayhead

Provides a media tracker with the current media playhead. For accurate tracking, call this method multiple times when the playhead changes.

| Variable Name | Description |
| :--- | :--- |
| `time` | Current playhead in seconds. For video-on-demand \(VOD\), the value is specified in seconds from the beginning of the media item. For live streaming, returns the playhead position if available or the current UTC time in seconds if not available. |

{% tabs %}
{% tab title="Android" %}
#### updateCurrentPlayhead

**Syntax**

```java
public void updateCurrentPlayhead(double time);
```

**Example**

```java
_tracker.updateCurrentPlayhead(1);
```
{% endtab %}

{% tab title="iOS" %}
#### updateCurrentPlayhead

**Syntax**

```objectivec
- (void) updateCurrentPlayhead: (double) time;
```

**Example**

Here are examples in Objective C and Swift:

**Objective C**

```objectivec
[_tracker updateCurrentPlayhead:1];
```

**Swift**

```swift
_tracker.updateCurrentPlayhead(1)
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

#### updateCurrentPlayhead

```jsx
tracker.updateCurrentPlayhead(1);
```
{% endtab %}
{% endtabs %}

### updateQoEObject

Provides the media tracker with the current QoE information. For accurate tracking, call this method multiple times when the media player provides the updated QoE information.

| Variable Name | Description |
| :--- | :--- |
| `qoeObject` | Current QoE information that was created by using the [createQoEObject](media-api-reference.md#createqoeobject) method. |

{% tabs %}
{% tab title="Android" %}
#### updateQoEObject

**Syntax**

```java
public void updateQoEObject(Map<String, Object> qoeObject);
```

**Example**

```java
HashMap<String, Object> qoeObject = Media.createQoEObject(1000000L, 2D, 25D, 10D);
_tracker.updateQoEObject(qoeObject);
```
{% endtab %}

{% tab title="iOS" %}
#### updateQoEObject

**Syntax**

```objectivec
- (void) updateQoEObject: (NSDictionary* _Nonnull) qoeObject;
```

**Example**

Here are examples in Objective C and Swift:

**Objective C**

```objectivec
NSDictionary* qoeObject = [ACPMedia createQoEObjectWithBitrate:1000000 startupTime:2 fps:25 droppedFrames:10];
[_tracker updateQoEObject:qoeObject];
```

**Swift**

```swift
let qoeObject = ACPMedia.createQoEObject(withBitrate: 1000000, startupTime: 2, fps: 25, droppedFrames: 10)
_tracker.updateQoEObject(qoeObject)
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

#### updateQoEObject

```jsx
let qoeObject = ACPMedia.createQoEObject(1000000, 2, 25, 10);
tracker.updateQoEObject(qoeObject);
```
{% endtab %}
{% endtabs %}

## Media constants

### Media type

Defines the type of a media that is currently tracked.

{% tabs %}
{% tab title="Android" %}
```java
public class Media {

  public enum MediaType {
      /**
      * Constant defining media type for Video streams
      */
      Video,

      /**
      * Constant defining media type for Audio streams
      */
      Audio
  }

}
```
{% endtab %}

{% tab title="iOS" %}
```objectivec
typedef NS_ENUM(NSInteger, ACPMediaType) {
    /**
    * Constant defining media type for Video streams
    */
    ACPMediaTypeVideo,

    /**
    * Constant defining media type for Audio streams
    */
    ACPMediaTypeAudio
};
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

```jsx
import {ACPMediaType} from '@adobe/react-native-acpmedia';

ACPMediaType.Video
ACPMediaType.Audio
```
{% endtab %}
{% endtabs %}

### Stream type

Defines the stream type of the content that is currently tracked.

{% tabs %}
{% tab title="Android" %}
```java
public class MediaConstants {

  public static final class StreamType {
      /**
      * Constant defining stream type for VOD streams
      */
      public static final String VOD = "vod";

      /**
      * Constant defining stream type for Live streams
      */
      public static final String LIVE = "live";

      /**
      * Constant defining stream type for Linear streams
      */
      public static final String LINEAR = "linear";

      /**
      * Constant defining stream type for Podcast streams
      */
      public static final String PODCAST = "podcast";

      /**
      * Constant defining stream type for Audiobook streams
      */
      public static final String AUDIOBOOK = "audiobook";

      /**
      * Constant defining stream type for AOD streams
      */
      public static final String AOD = "aod";
  }

}
```
{% endtab %}

{% tab title="iOS" %}
```objectivec
/**
 * Constant defining stream type for VOD streams
 */
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaStreamTypeVod;

/**
 * Constant defining stream type for Live streams
 */
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaStreamTypeLive;

/**
 * Constant defining stream type for Linear streams
 */
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaStreamTypeLinear;

/**
 * Constant defining stream type for Podcast streams
 */
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaStreamTypePodcast;

/**
 * Constant defining stream type for Audiobook streams
 */
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaStreamTypeAudiobook;

/**
 * Constant defining stream type for AOD streams
 */
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaStreamTypeAod;
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

```jsx
import {ACPMediaConstants} from '@adobe/react-native-acpmedia';

ACPMediaConstants.ACPMediaStreamTypeVod
ACPMediaConstants.ACPMediaStreamTypeLive
ACPMediaConstants.ACPMediaConstantsACPMediaStreamTypeLinear
ACPMediaConstants.ACPMediaStreamTypePodcast
ACPMediaConstants.ACPMediaStreamTypeAudiobook
ACPMediaConstants.ACPMediaStreamTypeAod
```
{% endtab %}
{% endtabs %}

### Standard video constants

Defines the standard metadata keys for video streams.

{% tabs %}
{% tab title="Android" %}
```java
public class MediaConstants {

  public static final class VideoMetadataKeys {
      public static final String SHOW = "a.media.show";
      public static final String SEASON = "a.media.season";
      public static final String EPISODE = "a.media.episode";
      public static final String ASSET_ID = "a.media.asset";
      public static final String GENRE = "a.media.genre";
      public static final String FIRST_AIR_DATE = "a.media.airDate";
      public static final String FIRST_DIGITAL_DATE = "a.media.digitalDate";
      public static final String RATING = "a.media.rating";
      public static final String ORIGINATOR = "a.media.originator";
      public static final String NETWORK = "a.media.network";
      public static final String SHOW_TYPE = "a.media.type";
      public static final String AD_LOAD = "a.media.adLoad";
      public static final String MVPD = "a.media.pass.mvpd";
      public static final String AUTHORIZED = "a.media.pass.auth";
      public static final String DAY_PART = "a.media.dayPart";
      public static final String FEED = "a.media.feed";
      public static final String STREAM_FORMAT = "a.media.format";
  }

}
```
{% endtab %}

{% tab title="iOS" %}
```objectivec
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyShow;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeySeason;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyEpisode;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyAssetId;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyGenre;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyFirstAirDate;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyFirstDigitalDate;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyRating;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyOriginator;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyNetwork;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyShowType;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyAdLoad;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyMvpd;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyAuthorized;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyDayPart;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyFeed;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyStreamFormat;
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

```jsx
import {ACPMediaConstants} from '@adobe/react-native-acpmedia';

ACPMediaConstants.ACPVideoMetadataKeyShow
ACPMediaConstants.ACPVideoMetadataKeySeason
ACPMediaConstants.ACPVideoMetadataKeyEpisode
ACPMediaConstants.ACPVideoMetadataKeyAssetId
ACPMediaConstants.ACPVideoMetadataKeyGenre
ACPMediaConstants.ACPVideoMetadataKeyFirstAirDate
ACPMediaConstants.ACPVideoMetadataKeyFirstDigitalDate
ACPMediaConstants.ACPVideoMetadataKeyRating
ACPMediaConstants.ACPVideoMetadataKeyOriginator
ACPMediaConstants.ACPVideoMetadataKeyNetwork
ACPMediaConstants.ACPVideoMetadataKeyShowType
ACPMediaConstants.ACPVideoMetadataKeyAdLoad
ACPMediaConstants.ACPVideoMetadataKeyMvpd
ACPMediaConstants.ACPVideoMetadataKeyAuthorized
ACPMediaConstants.ACPVideoMetadataKeyDayPart
ACPMediaConstants.ACPVideoMetadataKeyFeed
ACPMediaConstants.ACPVideoMetadataKeyStreamFormat
```
{% endtab %}
{% endtabs %}

### Standard audio constants

Defines the standard metadata keys for audio streams.

{% tabs %}
{% tab title="Android" %}
```java
public class MediaConstants {

  public static final class AudioMetadataKeys {
    public static final String ARTIST = "a.media.artist";
    public static final String ALBUM = "a.media.album";
    public static final String LABEL = "a.media.label";
    public static final String AUTHOR = "a.media.author";
    public static final String STATION = "a.media.station";
    public static final String PUBLISHER = "a.media.publisher";
  }

}
```
{% endtab %}

{% tab title="iOS" %}
```objectivec
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyArtist;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyAlbum;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyLabel;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyAuthor;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyStation;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyPublisher;
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

```jsx
import {ACPMediaConstants} from '@adobe/react-native-acpmedia';

ACPMediaConstants.ACPAudioMetadataKeyArtist
ACPMediaConstants.ACPAudioMetadataKeyAlbum
ACPMediaConstants.ACPAudioMetadataKeyLabel
ACPMediaConstants.ACPAudioMetadataKeyAuthor
ACPMediaConstants.ACPAudioMetadataKeyStation
ACPMediaConstants.ACPAudioMetadataKeyPublisher
```
{% endtab %}
{% endtabs %}

### Standard ad constants

Defines the standard metadata keys for ads.

{% tabs %}
{% tab title="Android" %}
```java
public class MediaConstants {

  public static final class AdMetadataKeys {
    public static final String ADVERTISER = "a.media.ad.advertiser";
    public static final String CAMPAIGN_ID = "a.media.ad.campaign";
    public static final String CREATIVE_ID = "a.media.ad.creative";
    public static final String PLACEMENT_ID = "a.media.ad.placement";
    public static final String SITE_ID = "a.media.ad.site";
    public static final String CREATIVE_URL = "a.media.ad.creativeURL";
  }

}
```
{% endtab %}

{% tab title="iOS" %}
```objectivec
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeyAdvertiser;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeyCampaignId;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeyCreativeId;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeyPlacementId;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeySiteId;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeyCreativeUrl;
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

```jsx
import {ACPMediaConstants} from '@adobe/react-native-acpmedia';

ACPMediaConstants.ACPAdMetadataKeyAdvertiser
ACPMediaConstants.ACPAdMetadataKeyCampaignId
ACPMediaConstants.ACPAdMetadataKeyCreativeId
ACPMediaConstants.ACPAdMetadataKeyPlacementId
ACPMediaConstants.ACPAdMetadataKeySiteId
ACPMediaConstants.ACPAdMetadataKeyCreativeUrl
```
{% endtab %}
{% endtabs %}

### Player State constants

Defines some common Player State constants.

{% tabs %}
{% tab title="Android" %}
```java
public class MediaConstants {

  public static final class PlayerState {
    public static final String FULLSCREEN = "fullscreen";
    public static final String PICTURE_IN_PICTURE = "pictureInPicture";
    public static final String CLOSED_CAPTION = "closedCaptioning";
    public static final String IN_FOCUS = "inFocus";
    public static final String MUTE = "mute";
  }

}
```
{% endtab %}

{% tab title="iOS" %}
```objectivec
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaPlayerStateFullScreen;
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaPlayerStatePictureInPicture;
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaPlayerStateClosedCaption;
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaPlayerStateInFocus;
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaPlayerStateMute;
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

```jsx
import {ACPMediaConstants} from '@adobe/react-native-acpmedia';

ACPMediaConstants.ACPMediaPlayerStateFullScreen
ACPMediaConstants.ACPMediaPlayerStatePictureInPicture
ACPMediaConstants.ACPMediaPlayerStateClosedCaption
ACPMediaConstants.ACPMediaPlayerStateInFocus
ACPMediaConstants.ACPMediaPlayerStateMute
```
{% endtab %}
{% endtabs %}

### Media events

Defines the type of a tracking event.

{% tabs %}
{% tab title="Android" %}
```java
public class Media {

    /**
    * These enumeration values define the type of a tracking event
    */
    public enum Event {
      /**
      * Constant defining event type for AdBreak start
      */
      AdBreakStart,

      /**
      * Constant defining event type for AdBreak complete
      */
      AdBreakComplete,

      /**
      * Constant defining event type for Ad start
      */
      AdStart,

      /**
      * Constant defining event type for Ad complete
      */
      AdComplete,

      /**
      * Constant defining event type for Ad skip
      */
      AdSkip,

      /**
      * Constant defining event type for Chapter start
      */
      ChapterStart,

      /**
      * Constant defining event type for Chapter complete
      */
      ChapterComplete,

      /**
      * Constant defining event type for Chapter skip
      */
      ChapterSkip,

      /**
      * Constant defining event type for Seek start
      */
      SeekStart,

      /**
      * Constant defining event type for Seek complete
      */
      SeekComplete,

      /**
      * Constant defining event type for Buffer start
      */
      BufferStart,

      /**
      * Constant defining event type for Buffer complete
      */
      BufferComplete,

      /**
      * Constant defining event type for change in Bitrate
      */
      BitrateChange,

      /**
      * Constant defining event type for State start
      */
      StateStart,

      /**
      * Constant defining event type for State end
      */
      StateEnd
  }

}
```
{% endtab %}

{% tab title="iOS" %}
```objectivec
/**
 * These enumeration values define the type of a tracking event
 */
typedef NS_ENUM(NSInteger, ACPMediaEvent) {
    /**
     * Constant defining event type for AdBreak start
     */
    ACPMediaEventAdBreakStart,
    /**
     * Constant defining event type for AdBreak complete
     */
    ACPMediaEventAdBreakComplete,
    /**
     * Constant defining event type for Ad start
     */
    ACPMediaEventAdStart,
    /**
     * Constant defining event type for Ad complete
     */
    ACPMediaEventAdComplete,
    /**
     * Constant defining event type for Ad skip
     */
    ACPMediaEventAdSkip,
    /**
     * Constant defining event type for Chapter start
     */
    ACPMediaEventChapterStart,
    /**
     * Constant defining event type for Chapter complete
     */
    ACPMediaEventChapterComplete,
    /**
     * Constant defining event type for Chapter skip
     */
    ACPMediaEventChapterSkip,
    /**
     * Constant defining event type for Seek start
     */
    ACPMediaEventSeekStart,
    /**
     * Constant defining event type for Seek complete
     */
    ACPMediaEventSeekComplete,
    /**
     * Constant defining event type for Buffer start
     */
    ACPMediaEventBufferStart,
    /**
     * Constant defining event type for Buffer complete
     */
    ACPMediaEventBufferComplete,
    /**
     * Constant defining event type for change in Bitrate
     */
    ACPMediaEventBitrateChange,
    /**
     * Constant defining event type for State start
     */
    ACPMediaEventStateStart
    /**
     * Constant defining event type for State end
     */
    ACPMediaEventStateEnd
};
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

```jsx
import {ACPMediaEvent} from '@adobe/react-native-acpmedia';

ACPMediaEvent.EventAdBreakStart
ACPMediaEvent.EventAdBreakComplete
ACPMediaEvent.EventAdStart
ACPMediaEvent.EventAdComplete
ACPMediaEvent.EventAdSkip
ACPMediaEvent.EventChapterStart
ACPMediaEvent.EventChapterComplete
ACPMediaEvent.EventChapterSkip
ACPMediaEvent.EventSeekStart
ACPMediaEvent.EventSeekComplete
ACPMediaEvent.EventBufferStart
ACPMediaEvent.EventBufferComplete
ACPMediaEvent.EventBitrateChange
ACPMediaEvent.EventStateStart
ACPMediaEvent.EventStateEnd
```
{% endtab %}
{% endtabs %}

### Media resume

Constant to denote that the current tracking session is resuming a previously closed session. This information **must** be provided when starting a tracking session.

{% tabs %}
{% tab title="Android" %}
#### Media resume

**Syntax**

```java
public class MediaConstants {

  public static final class MediaObjectKey {

      /**
      * Constant defining explicit media resumed property. Set this to true on MediaObject if resuming a previously closed session.
      */
      public static final String RESUMED;
  }

}
```

**Example**

```java
HashMap<String, Object> mediaObject = Media.createMediaObject("media-name", "media-id", 60D, MediaConstants.StreamType.VOD, Media.MediaType.Video);

// Attach media resumed information.
mediaObject.put(MediaConstants.MediaObjectKey.RESUMED, true);

_tracker.trackSessionStart(mediaObject, null);
```
{% endtab %}

{% tab title="iOS" %}
#### Media Resume

**Syntax**

```objectivec
  FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaKeyMediaResumed;
```

**Example**

Here are examples in Objective C and Swift:

**Objective C**

```objectivec
NSDictionary *mediaObject = [ACPMedia createMediaObjectWithName:@"media-name" mediaId:@"media-id" length:60 streamType:ACPMediaStreamTypeVod mediaType:ACPMediaTypeVideo];

// Attach media resumed information.
NSMutableDictionary *obj  = [mediaObject mutableCopy];
[obj setObject:@YES forKey:ACPMediaKeyMediaResumed];

[_tracker trackSessionStart:obj data:nil];
```

**Swift**

```swift
var mediaObject = ACPMedia.createMediaObject(withName: "media-name", mediaId: "media-id", length: 60, streamType: ACPMediaStreamTypeVod, mediaType:ACPMediaType.video)

// Attach media resumed information.
mediaObject[ACPMediaKeyMediaResumed] = true

_tracker.trackSessionStart(mediaObject, data: nil)
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

#### Media Resume

```jsx
let mediaObject = ACPMedia.createMediaObject("media-name", "media-id", 60, ACPMediaConstants.ACPMediaStreamTypeVod, ACPMediaType.Video);
mediaObject[ACPMediaConstants.ACPMediaKeyMediaResumed] = true

tracker.trackSessionStart(mediaObject, null);
```
{% endtab %}
{% endtabs %}

