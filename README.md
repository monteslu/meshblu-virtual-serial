meshblu-virtual-serial
======================

Virtual serial port running on top of skynet.im

#Use with Remote-IO!

https://github.com/monteslu/remote-io


# SkynetSerialPort

Use skynet to message a physical remote serial device:

```js
var SkynetSerialPort = require('skynet-serial').SerialPort;
var skynet = require('skynet');

// setup variables for myId, token, sendId
// the sendId is for the uuid of the physical serial device

var conn = skynet.createConnection({
  uuid: myId,
  token: token
});

conn.on('ready', function(data){
  var serialPort = new SkynetSerialPort(conn, sendId);
  var board = new firmata.Board(serialPort, function (err, ok) {
    if (err){ throw err; }
    //light up a pin
    board.digitalWrite(13, 1);
  });
});

```


# bindPhysical

Bind a physical serial port to recieve/push data from skynet:

```js
var SerialPort = require('serialport').SerialPort;
var bindPhysical = require('skynet-serial').bindPhysical;
var skynet = require('skynet');

// setup variables for myId, token, sendId
// the sendId should be for the uuid of the SkynetSerialPort app.

var conn = skynet.createConnection({
  uuid: myId,
  token: token
});

conn.on('ready', function(data){
  var serialPort = new SerialPort('/dev/tty.usbmodem1411',{
      baudrate: 57600,
      buffersize: 1
  });
  bindPhysical(serialPort, conn);
});

```
