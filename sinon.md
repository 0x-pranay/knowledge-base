# Sinon

## General 

## Fakes

## Spies

`spy.called` True if spy was called.

`spy.calledOnce` True if spy was called exactly once.

Check if first call threw an exception

`spy.firstCall.threw()`

get the returned value

`spy.firstCall.returnValue`

## Stubs

#### Reset a stubs behaviour

`var stub = sinon.stub();`

`stub.resetBehavior()`





-> Should include how to stub a dependency and restore it. With and without using sandbox

Issue: https://stackoverflow.com/questions/42148484/how-can-i-stub-internally-referenced-functions-with-sinonjs

https://stackoverflow.com/questions/35162659/sinon-function-stubbing-how-to-call-own-function-inside-module





## Sandbox

```
const sandbox = sinon.createSandbox()

// do stuff here

sandbox.restore()
```

