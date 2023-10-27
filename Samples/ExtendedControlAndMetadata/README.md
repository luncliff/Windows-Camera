# Sample UWP applications for using the [Windows Media Capture APIs](https://docs.microsoft.com/en-us/uwp/api/Windows.Media.Capture.MediaCapture) to interact with camera device controls and extract frame metadata from WinRT

This folder contains projects for sample applications that demonstrates the Windows Media Capture APIs:
- [```GetDeviceProperty()```](https://docs.microsoft.com/en-us/uwp/api/windows.media.devices.videodevicecontroller.getdeviceproperty?view=winrt-20348#Windows_Media_Devices_VideoDeviceController_GetDeviceProperty_System_String_)
- [```SetDeviceProperty()```](https://docs.microsoft.com/en-us/uwp/api/windows.media.devices.videodevicecontroller.setdeviceproperty?view=winrt-20348#Windows_Media_Devices_VideoDeviceController_SetDeviceProperty_System_String_System_Object_)
- [```GetDevicePropertyByExtendedId()```](https://docs.microsoft.com/en-us/uwp/api/windows.media.devices.videodevicecontroller.getdevicepropertybyextendedid?view=winrt-20348#Windows_Media_Devices_VideoDeviceController_GetDevicePropertyByExtendedId_System_Byte___Windows_Foundation_IReference_System_UInt32__)
- [```SetDevicePropertyByExtendedId()```](https://docs.microsoft.com/en-us/uwp/api/windows.media.devices.videodevicecontroller.setdevicepropertybyextendedid?view=winrt-20348#Windows_Media_Devices_VideoDeviceController_SetDevicePropertyByExtendedId_System_Byte___System_Byte___)
- [```MediaFrameReference::Properties()```](https://docs.microsoft.com/en-us/uwp/api/windows.media.capture.frames.mediaframereference.properties?view=winrt-20348#Windows_Media_Capture_Frames_MediaFrameReference_Properties)

Akin to how developers can interact with extended controls and metadata ([see this documentation](https://docs.microsoft.com/en-us/windows-hardware/drivers/stream/standardized-extended-controls-)), these WinRT APIs are used to interact with a camera device via [KSPROPERTY](https://docs.microsoft.com/en-us/previous-versions/ff564262(v=vs.85)), and in some case specifically with the ones related to [KSPROPERTYSETID_ExtendedCameraControl](https://docs.microsoft.com/en-us/windows-hardware/drivers/stream/kspropertysetid-extendedcameracontrol), in Windows 10.
While most camera controls are wrapped in their own APIs and accessed using the [VideoDeviceController](https://docs.microsoft.com/en-us/uwp/api/windows.media.devices.videodevicecontroller?view=winrt-20348), you can also send and receive payloads directly to and from the driver as raw byte buffers. While this has been done traditionaly in lower level code such as when writing drivers, this interaction is also possible from WinRT as shown in these samples. These raw buffers can then be serialized or deserialized according to a known format and projected for the application to use. This can be especialy useful if a driver exposes a custom control that requires a payload format known to the application or if an existing KSPROPERTY does not have its own wrapper API in WinRT.


## Available samples

- **[WinRT_ExtendedControlAndMetadataSample](./WinRT_ExtendedControlAndMetadataSample)**: sample containing a C# app and a C++/WinRT component showing how to
  - use ```GetDevicePropertyByExtendedId()``` and ```SetDevicePropertyByExtendedId()``` to set new extended camera controls that don't have dedicated APIs:
    - *KSPROPERTY_CAMERACONTROL_EXTENDED_EYEGAZECORRECTION*
    - *KSPROPERTY_CAMERACONTROL_EXTENDED_BACKGROUNDSEGMENTATION*
    - *KSPROPERTY_CAMERACONTROL_EXTENDED_FIELDOFVIEW2*
    - *KSPROPERTY_CAMERACONTROL_EXTENDED_FIELDOFVIEW2_CONFIGCAPS*
    - *KSPROPERTY_CAMERACONTROL_EXTENDED_FRAMERATE_THROTTLE*  
  - access and extract [frame capture metadata](https://docs.microsoft.com/en-us/windows-hardware/drivers/stream/mf-capture-metadata) (in this case *KSCAMERA_METADATA_BACKGROUNDSEGMENTATIONMASK*) using ```MediaFrameReference::Properties()```

- **[CPP-CLI_MediaCaptureSampleExtendedControl](./CPP-CLI_MediaCaptureSampleExtendedControl/)**: C++/CLI sample for using ```GetDeviceProperty()``` and ```SetDeviceProperty()``` to set common extended camera controls
