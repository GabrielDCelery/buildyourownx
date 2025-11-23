# Learning channels with AI

## Summary of lessons completed:

| Lesson | Topic                             |
| ------ | --------------------------------- |
| 1      | Basic Channel Creation            |
| 2      | Buffered Channels                 |
| 3      | Directional Channels              |
| 4      | Select Statement                  |
| 5      | Timeouts with select              |
| 6      | Done Channel Pattern              |
| 7      | Worker Pool                       |
| 8      | sync.WaitGroup                    |
| 9      | Fan-Out / Fan-In                  |
| 10     | Context for Cancellation          |
| 11     | Context with Timeout and Deadline |

For Lesson 12, here are some logical next topics that build on what you've learned:

1. errgroup - Handle errors from multiple goroutines elegantly (builds directly on context)
2. Rate Limiting - Use time.Ticker with channels to throttle operations
3. Semaphores - Limit concurrent goroutines using buffered channels
4. Graceful Shutdown - Combine OS signals with context for clean application termination
