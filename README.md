# WebRTC Android Static Library Builder

Builds `libwebrtc.a` (static library) for Android using GitHub Actions.
Designed for mediasoup-based projects that link WebRTC statically.

## Usage

1. Fork this repo
2. Go to **Actions** tab → **Build libwebrtc.a for Android**
3. Click **Run workflow**
4. Set branch: `branch-heads/7339` (M140) or `branch-heads/7559` (M144)
5. Set architectures: `armeabi-v7a,arm64-v8a`
6. Wait ~1 hour for build to complete
7. Download artifacts from the workflow run

## Output

- `libwebrtc.a` for each ABI (arm64-v8a, armeabi-v7a)
- WebRTC headers (api/, rtc_base/, sdk/android/, etc.)
- `libwebrtc.jar` (Java bindings)

## Integration with mediasoup Android SDK

```bash
# Copy to your SDK
cp lib/arm64-v8a/libwebrtc.a   deps/webrtc/lib/arm64-v8a/
cp lib/armeabi-v7a/libwebrtc.a deps/webrtc/lib/armeabi-v7a/
cp lib/libwebrtc.jar            deps/webrtc/lib/
# Replace headers
cp -r include/*                 deps/webrtc/src/
```

## GN Build Args

Same flags used by mediasoup:
- `use_rtti=true` (C++ RTTI for mediasoup)
- `use_custom_libcxx=false` (NDK STL compatibility)
- `rtc_use_h264=true` (H264 codec)
- `is_component_build=false` (static linking)
