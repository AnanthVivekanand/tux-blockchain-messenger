# TUXCOIN Blockchain Messages

A project for sending public messages through the tuxcoin blockchain.

Since ancient times, people have always tried to write messages that could last beyond human life.
Today everybody knows that cryptocurrencies are great to move and store money in an easy and secure, but less people are aware that you can also use these blockchains to write forever lasting immutable messages.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### How it works

Understanding this how this project functions will be helpful for development. This Github repository contains a **modified tuxcoin client** and a **HTML webpage**. The modified tuxcoin client has several additions to it that allow it to send messages through the blockchain.

##### The client
When a user sends a message using the modified client, the client embeds the text-based message inside a custom data-only transaction and then broadcasts it to the network. These messages use OP_RETURN (0x6a) to create data only transactions, these are also prefixed with 0xfeab to prevent collisions with other OP_RETURN transactions. When a user recieves a new transaction through the network, it can check to see if it is prefixed with 0xfeab and contains a message. The webpage in the above repository is a sample that will decode messages recieved on the blockchain.

##### The webpage
The webpage in the above repository is a viewer for messages sent with the modified client. It relies on a `insight-tux-api` websocket service running on a server somewhere. The client, when opened on a browser, can connect to the server through a websocket, through which transactions that the server recieves will also be forward to connected browsers. The connected browsers evaluate all real-time transactions that are sent through the websocket, which should be all of the transactions occuring on the network. If the client finds a transansaction prefixed with 0xfeab, then it will decode it and display the encoded message.

### Installing

When installing the project, you can either install the modified client or the HTML viewer or both.

##### The client

First install prerequsites for the client. To find preprequisites for your system, look in. If you have a debian-based system, you can do the following.
```
sudo apt-get install git
sudo apt-get install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils
sudo apt-get install libboost-system-dev libboost-filesystem-dev libboost-chrono-dev libboost-program-options-dev libboost-test-dev libboost-thread-dev
sudo apt-get install libboost-all-dev
sudo apt-get install software-properties-common
sudo add-apt-repository ppa:bitcoin/bitcoin
sudo apt-get update
sudo apt-get install libdb4.8-dev libdb4.8++-dev
sudo apt-get install libminiupnpc-dev
sudo apt-get install libzmq3-dev
sudo apt-get install libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler
```

To then compile the wallet, run
```
git clone https://github.com/KorkyMonster/tux-blockchain-messager.git
cd tux-blockchain-messager.
cd tuxcoin-modified-V2
./autogen.sh
./configure
make
```

The client can then be run by navigating to the `src` or `src/qt` folder and running `./tuxcoin-cli` or `./tuxcoin-qt`. `./tuxcoin-qt` will launch the graphical wallet. To use the messager from there, navigate to the wallet console and type `sendmessage "Hello World"`. You can replace 'Hello World!' with your custom message.

End with an example of getting some data out of the system or using it for a little demo

##### The HTML viewer

Simply opening it in the browser or replacing the websocket address will be enough. The webpage requires a insight-tux-api server, otherwise The webpage is ready as-is. For deloyment, store the file on a web server, to access it through a browser.

## Sending the message

To send a message, you must first compile the included modified wallet. To compile, follow the instructions above. A message can then sent by using `./tuxcoin-qt` in the src/qt folder or `./tuxcoin-cli` in the src folder.

#### `./tuxcoin-cli`

`tuxcoin-cli` can be found in the src folder. To send a message using it, run `sendmessage “<message>”`

```sendmessage “Hello world!”```

![tuxcoin-cli sending a message](http://i.imgur.com/BWkFBwJ.png)
#### `./tuxcoin-qt`

`tuxcoin-qt` can be found in the src/qt folder. Tuxcoin-qt is the graphical wallet, and it’s messaging features can be accessed throught the built-in console. Open the console and send a message by using `sendmessage “<message>”’.

![tuxcoin-qt wallet sending a message](http://i.imgur.com/SXJWoG3.png)
## Deployment

It is advised that the `insight-tux-api` is run from a dedicated web server, as well as the HTML web viewer, as it can recieve some stress.


## Contributing

If you have any ideas or contributions, feel free to open a pull request. I'll look over things as soon as I have the chance.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

