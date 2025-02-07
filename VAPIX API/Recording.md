# Recording API

* Typically used to retrieve a recording list or search for recording information by time. It can also be used to start, stop, or remove recordings.
* The date and time format used in the Recording API follows the UTC combined date and time format defined by ISO 8601: `<yyyy>-<mm>-<dd>T<HH>:<MM>:<SS>Z`. The fractional seconds information is optional.
<br/>

## Get Recording List
GET `https://${HOST}/axis-cgi/record/list.cgi?recordingid=all`

Response

```xml
<?xml version="1.0"?>
<root xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="http://www.axis.com/vapix/http_cgi/recording/list1.xsd">
    <recordings totalnumberofrecordings="1" numberofrecordings="1">
        <recording diskid="NetworkShare" recordingid="20240621_151725_95E7_B8A44F9D7D55" starttime="2024-06-21T07:17:25.349296Z" starttimelocal="2024-06-21T15:17:25.349296+08:00" stoptime="2024-06-21T07:18:17.615961Z" stoptimelocal="2024-06-21T15:18:17.615961+08:00" recordingtype="continuous" eventid="continuous" eventtrigger="continuous" recordingstatus="completed" source="1" locked="No">
            <video mimetype="video/x-h264" width="1920" height="1080" framerate="30:1" resolution="1920x1080"/>
        </recording>
    </recordings>
</root> 
```

<br/>

### Get Recording List with time query
GET `https://${HOST}/axis-cgi/record/list.cgi?starttime=2024-10-23T00:00:00&stoptime=2024-10-25T23:59:00`
(UTC ISO 8601 combined date and time)

Argument: `starttime`, `stoptime`, ...

Response

```xml
<?xml version="1.0"?>
<root xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="http://www.axis.com/vapix/http_cgi/recording/list1.xsd">
    <recordings totalnumberofrecordings="3" numberofrecordings="2">
        <recording diskid="NetworkShare" recordingid="20241023_101735_6B94_B8A44FB7B878" starttime="2024-10-23T02:17:35.937374Z" starttimelocal="2024-10-23T10:17:35.937374+08:00" stoptime="2024-10-23T02:18:07.095811Z" stoptimelocal="2024-10-23T10:18:07.095811+08:00" recordingtype="continuous" eventid="continuous" eventtrigger="continuous" recordingstatus="recording" source="1" locked="No">
            <video mimetype="video/x-h264" width="1920" height="1080" framerate="30:1" resolution="1920x1080"/>
        </recording>
        <recording diskid="NetworkShare" recordingid="20241023_101233_EAA5_B8A44FB7B878" starttime="2024-10-23T02:12:33.505337Z" starttimelocal="2024-10-23T10:12:33.505337+08:00" stoptime="2024-10-23T02:16:05.504428Z" stoptimelocal="2024-10-23T10:16:05.504428+08:00" recordingtype="continuous" eventid="continuous" eventtrigger="continuous" recordingstatus="completed" source="1" locked="No">
            <video mimetype="image/jpeg" width="1920" height="1080" framerate="30:1" resolution="1920x1080"/>
        </recording>
    </recordings>
</root>
```

## Start Recording
GET `https://${HOST}/axis-cgi/record/record.cgi?diskid=NetworkShare`

Response
```xml
<?xml version="1.0" encoding="utf-8"?>
<root xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="http://www.axis.com/vapix/http_cgi/recording/record1.xsd">
    <record recordingid="20240709_125955_7F35_B8A44F9D7D55" result="OK"/>
</root>
```

<span style="color:rgb(58, 231, 58);">Info:</span> AXIS cameras can perform multiple recordings simultaneously. Therefore, when stopping a recording, ensure that you input the correct recording ID.

<br/>

## Stop Recording
GET `https://${HOST}/axis-cgi/record/stop.cgi?diskid=NetworkShare&recordingid=${RecordingID}`

Response
```xml
<?xml version="1.0" encoding="utf-8"?>
<root xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="http://www.axis.com/vapix/http_cgi/recording/stop1.xsd">
    <stop recordingid="20240709_125955_7F35_B8A44F9D7D55" result="OK"/>
</root>
```
<br/>

## Remove Recording
GET `https://${HOST}/axis-cgi/record/remove.cgi?recordingid=${RecordingID}`

Response
```xml
<?xml version="1.0"?>
<root xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="http://www.axis.com/vapix/http_cgi/recording/remove1.xsd">
    <remove recordingid="20240709_125955_7F35_B8A44F9D7D55" result="OK"/>
</root>
```

<br/>

## Play Recording
For more details, please refer to [Media Stream](/Media%20Stream/media-stream-library-js.md).

<br/>

## Reference
[Edge Storage API - List recordings](https://developer.axis.com/vapix/network-video/edge-storage-api#list-recordings)