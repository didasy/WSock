#Created by Jesus Islam with MIT License

Dependencies : [lua-websockets](https://github.com/lipp/lua-websockets), [middleclass](https://github.com/kikito/middleclass)

##Installation

--------------------------------------

For now, just place it in your Lua modules directory.

Example:
`/usr/local/share/lua/5.1`

##Usage example

--------------------------------------

To create a simple websocket server with only one protocol named 'echo',
we could simply write this

`require 'WSock'

local server = WSock:new(9999, 60000)

local myproto = {
  echo = function (socket)
    socket:on_receive(function (socket, data)

      socket:write(math.random(999), server.socket.WRITE_TEXT)

    end)
  end
}

server:newProtocolHandler(myproto)

server:start()`

This server will listen at port 9999 on 127.0.0.1 or localhost, if you connect to it and send something, it would respond back with a random number ranged 1-999.


##A Little Documentation

-------------------------------------

####WSock:new(port, timeout)
`port` must be a number ranged 1-65535, while `timeout` must be a number too in miliseconds

####WSock:newProtocolHandler(protocol, handler)
`protocol` must be a string, while handler must be a function with a single argument to be used as new websocket instance.
For further information about available methods for websocket instance, see [here.](https://github.com/lipp/lua-websockets#websocket-methods)

####WSock:newProtocolHandler(protocolHandlerTable)
Same as above, but instead wrap the protocol and handler in a single table. For example:
`local myproto = {
  echo = function (socket)
    socket:on_receive(function (socket, data)

      socket:write(math.random(999), server.socket.WRITE_TEXT)

    end)
  end
}`

####WSock:start()
You need to it after you've done with the configuration.