### How does the DevBoard handle received serial messages? How does this differ from the naïve approach?
The DevBoard handles a received serial message by using a callback. By using a callback, the code isn't heavily reliant on the 
void loop() section of the Arduino code, and it allows you to establish a serial connection between the Python and Arduino code. 
By doing this, the Arduino becomes purely reactive, and not reliant on receiving a serial message, hence the reason why we didn't need 
any code inside the void loop portion of the Arduino code. The naive approach is to always read the received serial message, but that wastes a lot of energy compared to the prior method. 
### What does `detached_callback` do? What would happen if it wasn't used?
'detached_callback' is a helper decorator that will allow us to mark functions that we want to be spawned in a detached thread. 
A detached thread is allowed to be executed independently from the rest of the program, without having to wait for the rest of
the program to compile. If we didn't use 'detached_callback', the UI would just freeze if any serial code gets stuck or takes a long time to run. 
### What does `LockedSerial` do? Why is it _necessary_?
'LockedSerial' allows for a way to synchronize the access within a multithreaded environment. Because multiple threads could try to use the serial port at once, we want to prevent any undefined behavior from happening. To prevent this behvaior, we want to wrap the Serial object in a lock. 