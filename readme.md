![Inter-Process Communication](picture.png)

# LDPL CIPC Library
This is the LDPL CIPC (_Crappy Inter-Process Communication_) library. It's designed to
allow [LDPL](https://github.com/lartu/ldpl) programs to communicate with each other. It's far from perfect. It's enough for
my usecase. Use it at your own risk!

## Usage
The idea behind LDPL CIPC is that you have multiple channels that processes can use
to send messages to each other. A process can write messages into a channel, and another
process can read them. This is mostly designed for 1-on-1 communication only. Channels
don't need to be predeclared; they are created the moment something is written to them.

`WRITE <message> TO CHANNEL <channel_id>` is used to *send* a message to another process.
It effectively writes the message `<message>` of type **TEXT** to the channel of id
`<channel_id>`, also of type **TEXT**.

`READ CHANNEL <channel_id> IN <text_variable>` is used to *read* the contents of a channel
into a **TEXT** variable. The id of the channel to be read is `<channel_id>`, also of type **TEXT**.

## How does this work?
`mkdir` is atomic and fails if the folder already exists. I use it to create lockfiles for
the channels. Please use sensible channel names.

Also, think of channels as pipes or streams. You write values into them, and when you read
them, you get all that's in them at once. So if you write "Hi" and then "Hi", you'll get
"HiHi" when reading from it.

## How do I add this to my project?
`INCLUDE "cipc.ldpl"` and you are ready to go.

## License
MIT
