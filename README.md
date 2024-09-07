
# HTTP Live Streaming

This project provides a mechanism for video transcoding using HTTP Live Streaming (HLS). It segments video files using FFmpeg and uploads the segments along with an index file to a Wasabi bucket. Video.js is used for playing the video by referencing the index file.

## Features
- **Video Segmentation**: A Docker image is provided that uses FFmpeg to segment videos into chunks.
- **HLS Streaming**: Videos are uploaded as segments to a Wasabi bucket and played using Video.js.
- **Scalable Storage**: Video segments and index files are stored on Wasabi, an S3-compatible storage platform.
- **Video Playback**: The videos can be played by passing the URL of the index file to Video.js.

## Future Scope
- **Adaptive Bitrate Streaming**: Implement adaptive bitrate streaming based on the user's device and internet speed, optimizing the video experience for each user.

## Prerequisites
- Docker
- FFmpeg
- Video.js
- Wasabi Storage Account

## Getting Started

### 1. Clone the Repository
```bash
 git clone https://github.com/alokranjan609/Http-Live-Streaming.git
 cd video-transcoding-mechanism
 ```

### 2. Build the Docker Image
```bash
 docker build -t video-segmentation .
```

### 3. Run the Docker Container
```bash
 docker run -it video-segmentation
```

### 4.Inside the Docker container
Run the following command
```bash
 ffmpeg -i input.mp4  -codec:v libx264 -codec:a aac -hls_time 10 -hls_playlist_type vod -hls_segment_filename "${outputPath}/segment%03d.ts" -start_number 0 ${hlsPath}
```

### 5. Upload Segments and Index File to Wasabi Bucket
After segmentation, upload the contents of the \`segments\` folder and the \`index.m3u8\` file to your Wasabi bucket.

### 6. Play Video with Video.js
To play the video, pass the URL of the index file to Video.js:

```html
 <video id="my-video" class="video-js" controls preload="auto" width="640" height="264">
  <source src="https://your-wasabi-bucket.s3.wasabisys.com/path-to-index-file/index.m3u8" type="application/x-mpegURL">
 </video>
 <script src="https://vjs.zencdn.net/7.11.4/video.js"></script>
```

### 6. Future Enhancements
In the future, adaptive bitrate streaming will be implemented to provide a more seamless video experience based on the user's device and network speed.

## Technologies Used
- **FFmpeg**: For video segmentation into HLS chunks.
- **Docker**: To encapsulate the video segmentation process.
- **Video.js**: For video playback using the HLS protocol.
- **Wasabi**: For scalable, S3-compatible storage.

## Contributing
Contributions are welcome! Feel free to raise issues or submit pull requests.


