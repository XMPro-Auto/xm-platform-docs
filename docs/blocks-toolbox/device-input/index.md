# Device Input Blocks

Device Input blocks allow users to interact with your XMPro applications using various device capabilities, such as cameras and location services. These blocks enable the capture of real-world data directly through the user's device.

## Available Device Input Blocks

- [Location Capture](location-capture.md) - Captures the user's geographical location using the device's GPS or network-based location services
- [Visual Media Capture](visual-media-capture.md) - Captures photos or videos using the device's camera

## Best Practices for Using Device Input Blocks

1. **Request permissions appropriately**: Device input blocks often require specific permissions from the user (e.g., camera access, location access). Ensure that your application requests these permissions at the appropriate time and provides clear explanations of why they are needed.

2. **Handle permission denials gracefully**: Users may deny permission for your application to access certain device features. Your application should handle these situations gracefully and provide alternative ways for users to accomplish their tasks.

3. **Consider device capabilities**: Not all devices have the same capabilities. Some may have multiple cameras, while others may have limited or no location services. Design your application to adapt to the available device capabilities.

4. **Optimize for performance**: Capturing and processing device input can be resource-intensive. Optimize your application to minimize battery drain and ensure smooth performance.

5. **Provide feedback**: Give users clear feedback when device input is being captured or processed. This helps users understand what's happening and can improve the overall user experience.

6. **Respect privacy**: Be transparent about how device input data is used and stored. Only capture the data you need, and ensure that sensitive data is handled securely.

7. **Test on multiple devices**: Test your application on a variety of devices to ensure that device input blocks work correctly across different hardware and software configurations.

## Examples

### Location-Based Asset Tracking

```
Box (Asset Tracking Container)
├── Location Capture
│   ├── Button (Capture Location)
├── Field (Asset ID)
│   ├── Textbox
├── Field (Asset Name)
│   ├── Textbox
├── Field (Asset Type)
│   ├── Select Box
├── Field (Notes)
│   ├── Text Area
├── Box (Buttons)
│   ├── Button (Save)
│   ├── Button (Cancel)
```

### Field Inspection with Photo Documentation

```
Box (Inspection Container)
├── Field (Inspection ID)
│   ├── Textbox
├── Field (Inspector)
│   ├── Textbox
├── Field (Date)
│   ├── Date Selector
├── Visual Media Capture
│   ├── Button (Take Photo)
│   ├── Image (Preview)
├── Field (Condition)
│   ├── Select Box
│       ├── Option (Good)
│       ├── Option (Fair)
│       ├── Option (Poor)
├── Field (Notes)
│   ├── Text Area
├── Box (Buttons)
│   ├── Button (Submit)
│   ├── Button (Save Draft)
```

### Mobile Data Collection

```
Box (Data Collection Container)
├── Location Capture
│   ├── Button (Capture Location)
│   ├── Map (Location Preview)
├── Visual Media Capture
│   ├── Button (Take Photo)
│   ├── Image (Preview)
├── Field (Sample ID)
│   ├── Textbox
├── Field (Sample Type)
│   ├── Select Box
├── Field (Measurements)
│   ├── Number Selector
├── Field (Observations)
│   ├── Text Area
├── Box (Buttons)
│   ├── Button (Submit)
│   ├── Button (Save Draft)
```

By effectively using device input blocks, you can create applications that leverage the capabilities of modern devices to capture and process real-world data, enabling a wide range of use cases from field inspections to asset tracking and beyond.
