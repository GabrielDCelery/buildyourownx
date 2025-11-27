# Lesson 22: Bridge Pattern - Flatten Channel of Channels

Concept: Take a channel that receives channels and flatten all values into a single output channel. Useful when workers dynamically create result
channels.

Your task:

1. bridge(ctx, chanOfChans) <-chan T - Flattens channel of channels
   - Input: <-chan (<-chan T) - a channel that receives channels
   - Output: <-chan T - single channel with all values
   - For each channel received, read all its values
   - Send all values to single output
   - Respects context cancellation
   - Closes output when input closes AND all sub-channels are drained

2. worker(id, ctx) <-chan int - Simulates dynamic worker
   - Returns a channel
   - Sends 3-5 values with delays
   - Prints "worker X: value Y"

3. In main():
   - Create channel of channels: chanOfChans := make(chan (<-chan int))
   - Spawn goroutine that creates 3 workers dynamically
   - Send each worker's channel into chanOfChans
   - Close chanOfChans after all workers sent
   - Use bridge(ctx, chanOfChans) to flatten
   - Print all received values
   - Context with 5 second timeout

Expected output:
worker 1: 0
worker 2: 0
worker 3: 0
received: 0
received: 0
worker 1: 1
received: 0
worker 2: 1
...

Key challenge: You need to spawn a goroutine for each sub-channel received to drain it concurrently. Use a WaitGroup to know when all are done.

##

Example scenario:

```go
// Worker creates a channel of results
func worker() <-chan int { ... }

// You spawn 5 workers dynamically
workerChannels := make(chan (<-chan int))
go workerChannels <- worker() // Send channels into the channel!

// Bridge flattens all worker outputs into one
output := bridge(ctx, workerChannels)
```
