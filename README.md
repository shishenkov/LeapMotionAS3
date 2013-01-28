[LeapMotionAS3](http://github.com/logotype/LeapMotionAS3)
=================

This is the AS3 framework for working with the Leap.

Created and maintained by [Victor Norgren](http://logotype.se)

Quick start
-----------

Clone the repo, `git clone git://github.com/logotype/LeapMotionAS3.git`.

Create an instance of the LeapMotion class (called Controller in the official docs)

    leap = new LeapMotion();
    leap.data.addEventListener( LeapMotionEvent.LEAPMOTION_INIT, onInit );
    leap.data.addEventListener( LeapMotionEvent.LEAPMOTION_CONNECTED, onConnect );
    leap.data.addEventListener( LeapMotionEvent.LEAPMOTION_DISCONNECTED, onDisconnect );
    leap.data.addEventListener( LeapMotionEvent.LEAPMOTION_EXIT, onExit );
    leap.data.addEventListener( LeapMotionEvent.LEAPMOTION_FRAME, onFrame );

What you'll get from the LEAPMOTION_FRAME handler is a Frame object, with strongly
typed properties such as Hand, Pointables, Direction and much more:

    public function onFrame( event:LeapMotionEvent ):void
    {
    	// Get the most recent frame and report some basic information
    	var frame:Frame = event.frame;
    	trace("Frame id: " + frame.id + ", timestamp: " + frame.timestamp + ", hands: " + frame.hands.length + ", fingers: " + frame.fingers.length + ", tools: " + frame.tools.length);
    
    	if ( frame.hands.length > 0 )
    	{
    		// Get the first hand
    		var hand:Hand = frame.hands[ 0 ];
    
    		// Check if the hand has any fingers
    		var fingers:Vector.<Pointable> = hand.fingers;
    		if ( !fingers.length == 0 )
    		{
    			// Calculate the hand's average finger tip position
    			var avgPos:Vector3 = new Vector3( 0, 0, 0 );
    			for each ( var finger:Finger in fingers )
    				avgPos = avgPos.plus( finger.tipPosition );
    
    			avgPos = avgPos.divide( fingers.length );
    			trace("Hand has " + fingers.length.toFixed( 2 ) + " fingers, average finger tip position: " + avgPos);
    		}
    
    		// Get the hand's sphere radius and palm position
    		trace("Hand sphere radius: " + hand.sphereRadius.toFixed( 2 ) + " mm, palm position: " + hand.palmPosition);
    
    		// Get the hand's normal vector and direction
    		var normal:Vector3 = hand.palmNormal;
    		var direction:Vector3 = hand.direction;
    
    		// Calculate the hand's pitch, roll, and yaw angles
    		trace("Hand pitch: " + LeapMath.toDegrees( direction.pitch()).toFixed( 2 ) + " degrees, " + "roll: " + LeapMath.toDegrees( normal.roll()).toFixed( 2 ) + " degrees, " + "yaw: " + LeapMath.toDegrees( direction.yaw()).toFixed( 2 ) + " degrees");
    	}
    }

Features
--------

+ Very similar structure as the official API
+ No dependencies, creates a optimized socket directly to the Leap
+ Compatible with Mac and PC

Upcoming features
-----------------

+ Multi-threading using Workers
+ Optional dispatch model using Signals
+ Examples

Authors
-------

**Victor Norgren**

+ http://twitter.com/logotype
+ http://github.com/logotype
+ http://logotype.se


Copyright and license
---------------------

Copyright © 2013 logotype

Author: Victor Norgren

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to
deal in the Software without restriction, including without limitation the
rights to use, copy, modify, merge, publish, distribute, sublicense, and/or
sell copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:  The above copyright
notice and this permission notice shall be included in all copies or
substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS
IN THE SOFTWARE. 
