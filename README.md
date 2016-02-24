var express = require('express');
var net = require('net');
var app = express();
var sock;

//first of all connect to a stable client
console.log('waiting for connection\nfrom mobile server on port 5132');
var server = net.createServer(function(socket) { sock = socket; });
server.listen(5132);

//receive request from other clients
app.get('/', function (req, res) 
{
	// retriving mobileNumber and message
	console.log('A new request\nreceived on 6544 ');
	var mobileNumber = req.query.mobileNumber;
	var message      = req.query.message;
	
    if (sock) 
    {
    	sock.write(mobileNumber+"\n"+message+"\n");

    }
    
    res.end('i am ended');
});

app.listen(6544);
