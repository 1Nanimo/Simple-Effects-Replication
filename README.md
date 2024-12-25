A simple replication system

# Instalation
You need to move the ``Effects`` module to ``ReplicatedStorage`` and it is ready to use

OBS: **You must have required Modulo Effects on the server for the effect to be replicated.**


## To create an effect
Everything in ``FirstClientProcessData`` will be the client's first processing, you can use it for checks, creating hitboxes, etc..., and its return will be sent to the ``Client`` or ``Server``

```lua
return {
	FirstClientProcessData = function(paramAExample, paramBExample) --> Parameters passed in :Post()
		return paramAExample, paramBExample
	end,
	
	Client = function(...) --> Receive the paramAExample,paramBExample
		return ...
	end,
	
	Server = function(...) --> Receive the paramAExample,paramBExample
		return ...
	end,
}
```

## Client Post Effect
```lua
-->> Services
local ReplicatedStorage = game:GetService('ReplicatedStorage')

-->> Packages
local Effects = require(ReplicatedStorage.Packages.Effects)

-->> Example effect
Effects:Post('EffectNameModule', Vector3.new(1,1,1), Color3.new(0,0,0), 'StringTest'))

```

## Server Post Effect
```lua
-->> Services
local Players = game:GetService('Players')
local ReplicatedStorage = game:GetService('ReplicatedStorage')

-->> Packages
local Effects = require(ReplicatedStorage.Packages.Effects)

-->> Vars
local ExamplePlayer = Players.ExamplePlayer

-->> Example effect
Effects:Post(ExamplePlayer, 'EffectNameModule', Vector3.new(1,1,1), Color3.new(0,0,0), 'StringTest')) --> For only one player

-->> or for all players
Effects:PostAll(ExamplePlayer, 'EffectNameModule', Vector3.new(1,1,1), Color3.new(0,0,0), 'StringTest'))
```
