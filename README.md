# Video Doorbell, Lab 7

*A lab report by Fabio Daiber*

### In This Report

1. Upload a video of your version of the camera lab to your lab Github repository
1. As usual, update your class Hub repository to add your [forked IDD-Fa18-Lab7](/FAR-Lab/IDD-Fa18-Lab7) repository.
1. Answer the questions in-line below on your README.md.

## Part A. HelloYou from the Raspberry Pi

**a. Link to a video of your HelloYou sketch running.**

[Hello You running](https://drive.google.com/open?id=19aSEgs3In4nkqCfpJuAUOhAdIb4vtToG)

## Part B. Web Camera

Camera successfully connected: 

![alt text](https://github.com/fpdaiber/IDD-Fa19-Lab7/blob/master/Img01.png)

**a. Compare `helloYou/server.js` and `IDD-Fa18-Lab7/pictureServer.js`. What elements had to be added or changed to enable the web camera? (Hint: It might be good to know that there is a UNIX command called `diff` that compares files.)**

Below the difference between the two files when compared with `diff`. The webcam module had to be loaded and the webcam has to be setup to be able to take the pictures. Lastly, the 'take a picture' function has to be defined, so that the server can display the picture.

Excerpt from pi@ixe109:~ $ diff IDD-Fa19-Lab7/pictureServer.js helloYou/server.js

```

< //-- Addition:
< var NodeWebcam = require( "node-webcam" );// load the webcam module


< //----------------------------WEBCAM SETUP------------------------------------//
< //Default options
< var opts = { //These Options define how the webcam is operated.
<     //Picture related
<     width: 1280, //size
<     height: 720,
<     quality: 100,
<     //Delay to take shot
<     delay: 0,
<     //Save shots in memory
<     saveShots: true,
<     // [jpeg, png] support varies
<     // Webcam.OutputTypes
<     output: "jpeg",
<     //Which camera to use
<     //Use Webcam.list() for results
<     //false for default device
<     device: false,
<     // [location, buffer, base64]
<     // Webcam.CallbackReturnTypes
<     callbackReturn: "location",
<     //Logging
<     verbose: false
< };
< var Webcam = NodeWebcam.create( opts ); //starting up the webcam
< //----------------------------------------------------------------------------//
< 

<   //-- Addition: This function is called when the client clicks on the `Take a picture` button.
<   socket.on('takePicture', function() {
<     /// First, we create a name for the new picture.
<     /// The .replace() function removes all special characters from the date.
<     /// This way we can use it as the filename.
<     var imageName = new Date().toString().replace(/[&\/\\#,+()$~%.'":*?<>{}\s-]/g, '');
< 
<     console.log('making a making a picture at'+ imageName); // Second, the name is logged to the console.
< 
<     //Third, the picture is  taken and saved to the public/ folder
<     NodeWebcam.capture('public/'+imageName, opts, function( err, data ) {
<     io.emit('newPicture',(imageName+'.jpg')); ///Lastly, the new name is send to the client web browser.
<     /// The browser will take this new name and load the picture from the public folder.
<   });
< 
<   
```


**b. Include a video of your working video doorbell**

We had to put a sweater over the camera and I pressed the button because the camera lighting was so bad that you could not recognize anything:

![alt text](https://github.com/fpdaiber/IDD-Fa19-Lab7/blob/master/img02.png)

[Doorbell Video](https://drive.google.com/open?id=12x0e5TQA8i1Fh5pDagu1qmiF-QDo6l_8)

[My modified code](https://github.com/fpdaiber/IDD-Fa19-Lab7/blob/master/pictureServer_update.js)

## Part C. Make it your own

**a. Find, install, and try out a node-based library and try to incorporate into your lab. Document your successes and failures (totally okay!) for your writeup. This will help others in class figure out cool new tools and capabilities.**

**b. Upload a video of your working modified project**
