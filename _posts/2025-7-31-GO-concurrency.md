---
title: Concurrency
categories: [Golang, Basics]
tags: [] # TAG names should always be lowercase
---

## ✅ Goroutine

- **concurrent thread** managed by `Go runtime`
- can run function **concurrently** and **parallel**

- if a function is turned into a go routine,
- it runs in the background, concurrently

- 👍🏻 lightweight than OS thread
- ⚠️ if main function finishes before go routine, might not see output
- 💊 `time.Sleep(1 * time.Second)`
- 💊 `fmt.Scanln()`

```go
//create a go routine
//run this function in the background
//push function count into its own go routine

func main() {
    go count("sheep")
    go count("fish")

    //blocking code, wait
	//prevent main function from immediately terminating
	//give some time to go routines to run
    fmt.Scanln()
}


func count(thing string) {
    //count function
}
```

## ✅ Waitgroup

- Waitgroup: type from `Go sync package` to **wait for a collction of goroutines to finish**
- like a counter that tracks how many `goroutines` you are waiting for
- 👍🏻 allow `goroutines` to run and finish before exiting `main()`

```go
import(
    "sync"
)

func main() {
	var wg sync.WaitGroup //create waitgroup
	wg.Add(1) //counter increase ++

	go func() { //goroutine launch
		count("sheep")
		wg.Done() //decrease --
	}()

	wg.Wait() //block main routine until counter is 0
}
```

- `Add()`: increase the count
- `Done()`: decrease the count
- `Wait()`: block main function from terminating until count is 0

## ✅ Channel

- Channel: pipe for go functions to communicate, pipe to send messages
- channel also needs a type `c chan string` or `c := make(chan string)`
- sending/recieving message through a channel is a **blocking** operation
- 👍🏻 blocking nature of channel make synchonization possible for go routines
- 👍🏻 channel allow safe communiation & synchronization

- ⚠️ **Deadlock in channel**
- even when there are _no more_ message(i>5), main function will still wait for message
- 💊 use `close(c)` and 💊 `open boolean` to check if channel is open
- reciever should never close the channel

- ☑️ Example of channel use
- `c := make(chan string)` create channel
- `c <- "hello"`: send message to channel
- `message := <-c`: recieve message

```go
// message 5 times
func count(thing string, c chan string) {  //channel as param
	for i := 1; i <= 5; i++ {
		c <- thing //send thing as message through channel
		time.Sleep(time.Millisecond * 500)
	}

    //close the channel, prevent deadlock
	close(c)
}

func main(){
    c := make(chan string) //create channel
	go count("sheep", c)

	for {
		message, open := <-c //recive message comming out of the channel
		if !open {           //if no more message, break out of for loop
			break
		}
		fmt.Println(message) //print "sheep" 5 times
	}
}

```

- ☑️ **use `range` to get messages & prevent deadlock**

```go
    for message := range c { //iterate over channel
		fmt.Println(message)
	}
```

## ✅ Select in concurrency

- Select: when there are several channel operations, proceed with whichever is **ready first**
- like a switch statement for channels

- there are two `goroutines`
- (1) run every 500ms
- (2) run every 2000ms(2 seconds)
- (1) will be ready faster than (2)

- 👎🏻 without select: (2) will block (1)
- even (1) is ready, cannot run until (2) is finished
- 👍🏻 with select, (1) can run whenever it is ready, without waiting for (2)
- (1) can run more times

```go
c1 := make(chan string)
c2 := make(chan string)


	go func() {
		for {
			c1 <- "Every 500ms"
			time.Sleep(time.Millisecond * 500)
		}
	}()

	go func() {
		for {
			c2 <- "Every two seconds"
			time.Sleep(time.Millisecond * 2000)
		}
	}()

    // 👎🏻 without select
	// for {
	// 	fmt.Println(<-c1)
	// 	fmt.Println(<-c2)
	// }

    //result:
    //Every 500ms
    //Every two seconds

    // 👍🏻 with select
	for {


		select {
		case msg1 := <-c1:
			fmt.Println(msg1)
		case msg2 := <-c2:
			fmt.Println(msg2)
		}
	}
    //result:
    // Every 500ms
    // Every 500ms
    // Every 500ms
    // Every 500ms
    // Every two seconds
```

## ✅ Directional channels

- `c chan int`: can send and recive
- `c <-chan int`: recieve only
- `c chan<- int`: send only

## ✅ Jobs and workerpools

- job: queue/stack of jobs to do, `caculate fibo`
- worker: recieve jobs from job list and send result

```go
//jobs to do
func fibo(n int) int {
	if n <= 1 {
		return n
	}
	return fibo(n-1) + fibo(n-2)
}

// worker to recieve jobs
// jobs: recieve only
// results: send only
func worker(jobs <-chan int, results chan<- int) {
	for n := range jobs {
		results <- fibo(n)
	}
}

func main() {
	jobs := make(chan int, 100) //create 100 job channels
	results := make(chan int, 100) //create 100 results channels

	go worker(jobs, results) //launch goroutine

	for i := 0; i < 100; i++ { //create jobs
		jobs <- i
	}
	close(jobs)

	for j := 0; j < 100; j++ { //recieve results
		fmt.Println(<-results)
	}
}
```

## ✅

## ✅

## ✅
