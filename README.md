<h1 align="center">RRDownloadFile</h1>

Allows you to download file from url and store it in the memory. Available only for iOS 7.0+. You can pause, resume or cancel a download, when you want. It works also in background task, so you can download file when the application is in background or close by the user. RRDownloadFile uses NSURLSession for download the file.

<h3 align="center">Usage</h3>
Simple Download:

```swift
let url = NSURL(string: "https://developer.apple.com/library/ios/documentation/NetworkingInternetWeb/Conceptual/NetworkingOverview/NetworkingOverview.pdf")
        
RRDownloadFile.download("network.pdf", downloadSource: url!,
progressBlockCompletion: nil) { (error, fileDestination) -> () in
  if error == nil {
    println("file downloaded :\(fileDestination)")
  }
}
```

Trace the download progress

```swift
RRDownloadFile.download("network.pdf", downloadSource: url!, progressBlockCompletion: { (bytesWritten, bytesExpectedToWrite) -> () in
  println("progress :\(bytesWritten) / \(bytesExpectedToWrite)")
}) { (error, fileDestination) -> () in
  if error == nil {
    println("file downloaded :\(fileDestination)")
  }
}
```

Pause, resume, and cancel a download

```swift
let downloadTask = RRDownloadFile.download("network.pdf", downloadSource: url!, progressBlockCompletion: nil) { (error, fileDestination) -> () in
  if error == nil {
    println("file downloaded :\(fileDestination)")
  }
}
        
RRDownloadFile.pauseDownload(downloadTask: downloadTask)
RRDownloadFile.resumeDownload(downloadTask: downloadTask)
RRDownloadFile.cancelDownload(downloadTask: downloadTask)
```
You can change the destination of a download by passing the url in parameter. If the path doesn't exsit it will be created.

```swift
let customDestinationPath = NSURL(string: "Download/pdf")

RRDownloadFile.download("network.pdf", downloadSource: url!, pathDestination: customDestinationPath!, progressBlockCompletion: nil) { (error, fileDestination) -> () in
  //The file will be saved in DocumentDirectory/Download/pdf/network.pdf
}

```
