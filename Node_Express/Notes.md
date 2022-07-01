# 25 June 2022 - Day 21

- Run-Time Environment for JS
- Built on Chrome’s V8 JS Engine

### Browser vs Node

![image](https://user-images.githubusercontent.com/66965591/175787385-c45f6ccd-fec9-417b-a853-5d41acde048d.png)


### Global Variables

- As discussed we don’t have window variable in node
- But we got lots of other useful globals
    - To name a few:
    - module - info about the current module
    - require - function to use modules (CommonJS)
    - process - info about the env where the program is being executed

### Modules

- Encapsulated code (only share minimum)
- Node uses CommonJS Library under the hood , Every file is a module (by default)
- To share the data inside your module to the whole app, you need to export it.

```jsx
module.exports = {obj1, func1, var1, ....}
```

#! When you import a module, you actually invoke it.
Node wraps it in the function.

### NPM

`npm test`, `npm start`, `npm restart`, and `npm stop` are all aliases for `npm run xxx.`

For all other `scripts` you define, you need to use the `npm run xxx` syntax.

# 26 June 2022 - Day 22

Bigger Picture

![image](https://user-images.githubusercontent.com/66965591/175835464-ebb5fd6d-341b-40f0-928a-a7fe5212d011.png)

- So in here we have
- V8
    - JS Runtime
- WebAPIs
    - DOM, ajax, setTimeout, etc
- Callback Queue
    - callback functions queue
- Even Loop
    - when stack’s empty pushes the task from the callback queue to the stack

setTimeout is an API provided by the browser. It’s not in the V8. 

### !FUN-FACT

setTimeout() doesn’t guarantee that ur code will run in the given time but after at least the given time.


# 27 June 2022 - Day 23

### Multi-Tasking

- First there used to single core processors - only one program could run at once.
    - OS itself is a program. So, it would run, then you’d tell another program to start, then OS would have to stop to make the program run. And so the things worked.
    - Eg. MS-DOS, Apple 2C
- So, we then created cooperative multitasking.
    - Here the applications, after they have done their work would call mostly a function called yield. Which would signal the OS of completion/pause. So, OS would startup again and would be like - okay, so this is done , who else needs to run next?
    - If nothing then the OS would itself keep running.
    - Cons:
        - Dependent upon the application calling yield
            - So, if the app doesn’t call yield it would keep on running & never give anyone else a change to run
            - If the app ever crashes or something, with the app the whole system would go down.
    - Eg. Early windows - windows 95, windows98; Early macos - all the original versions of macos til macos 9
- Then we went to Preemptive Multitasking
    - The OS now has the ability to pause (save the app state) any app at any time.
    - Pros:
        - OS is handling things
        - Not dependent on user app
    - It has been in the unix n especially the Mainframe world from v.long.
    - But it came to the PC world a lil bit later.
    - Microsoft introduced this with their WindowsNT kernel
    - So, windowNT4 had this so did window200, More importantly was WindowsXP
    - In mac world too. They decided to rewrite the whole thing
    - And from the MacOS 10.0 - evolution of FreeBSD
- AMD released multi-core processors in the mid-2000s
- So, how can we harness these multi-core for better performance
- So after a lot of research we came up with → Systematic Multi-threading
- Intel was the 1st to market this tech.
    - And they branded it as Hyper Threading
- What’s new
    - The OS is able to take new instructions, where the OS can actually give some more info to the processor  on how to run things in parallel.
    - So, inside a modern processor we executed the instructions in stages.
        - Like we’ll give it some assembly instructions that says load this value or multiply these, etc. And it’ll break it down into steps.
        - And inside some of those steps in a processor, which is called a **pipeline.**
        - They actually have multiple copies of the parts of the process that do the thing we wanna do.
    - So, like modern processors (single processor), will have a thing called floating-point unit.
    And this is for doing fpu multiplication. But there’s actually more than one. There’s usually like 2-6 (depends on the processor).
    - So, like by using these new instructions, the OS is able to tell a processor that - hey, there’s this 2 things of code coming in. They’re actually from different thread. So, you don’t have to worry about doing all the normal safety checks. Just run them in parallel if you can.
    - So, this isn’t 2 completely separate CPU cores so not much of a speed difference. (15-20% - depends on kinda the code written)
    - So, these systems we’re finally able to really run a lot of different code simultaneously.

### Process vs Threads

![image](https://user-images.githubusercontent.com/66965591/176020483-e426703a-c0f0-46ea-988e-9f79a9d4844b.png)

### Nodejs is Single Threaded

(except when it’s not)

- All JS, V8, event loop run in the single Main Thread.
- It has like 2/3 JS to 1/3 C++ code ratio.
- C++ is different as it has access to threads.
    - But it depends on how it’s run
- So, if u have a js method that you’re calling from node it’s backed by a C++ method.
    - If it’s synchronous js call, then that c++ code will always run on the main thread.
    - If you’re calling an asynchronous methods from the js this method’s backed by C++.
    Sometimes, it runs on the main thread & sometimes it doesn’t.
        - It actually depends on the context in which you’re making this function call.
    

Calling Async Function In Node (for 2, 4, 6 times) (2 Core Processor)

![image](https://user-images.githubusercontent.com/66965591/176020511-a80f786a-8e50-4f08-8d99-cbc7c2dd9e25.png)

1. 2 Requests
    1. Same time for both.
2. 4 Requests
    1. Again same time but took longer.
        1. Reason being we only got 2 cores.
        2. So, it’ll assign 2 threads each. Thus, increasing the workload for a single processor & thus resulting in increase in runtime.
3. 6 Requests
    1. Hashing operations in C++ are done in a bg thread. But doesn’t spin up a new thread for each request.
    2. Instead whenever you first make a request for something that’s gonna go on a thread. It’ll automatically spin-up a preset number of threads (which defaults to 4).
    3. So, it’ll spin up these 4 threads & will constantly reuse those threads for all of its work.
    4.  This set of threads is what’s called the Thread Pool
    5. So, for the 5th & 6th requests, it puts them in a queue, until one of the worker threads become available & then the same thing with the 6th request.

Async Network Requests

![image](https://user-images.githubusercontent.com/66965591/176020555-646e510c-93ea-43bd-b6a0-e0d70070416b.png)

![image](https://user-images.githubusercontent.com/66965591/176020582-0e314159-1ed7-4b07-b54e-d36c863a6b75.png)

- Okay, so this is performed as per our previous observations.

![image](https://user-images.githubusercontent.com/66965591/176020612-b600d620-2814-442d-b7eb-09df2f9a639b.png)

- But here, we can see that even in 4 requests there’s non time increase see, unlike our previous case.
- Reason is that this is nothing to do with node.
- This is all about the kind of the computer architecture & bottlenecks.
- When we’re download a file (not writing to hdd) - the limitation is the network itself.
    - As whenever we’re downloading a file like this our computer is basically just sitting doing nothing most of the time. And every once in a while it gets a lil bit of data from the network which will then go to the processor.
    - So, since we’re not limited by the no. of cpu cores, we don’t reach that bottleneck & there’s no time difference.

![image](https://user-images.githubusercontent.com/66965591/176020662-5f7ae79d-631f-41f7-9eb5-2440ad160b7e.png)

- This is again is unexpected from our previous case. There’s no tail.
- It turns out that this is actually not subjected to the limitations of the thread pool.
- Reason is that inside of node, whenever possible it’ll actually use C++ asynchronous primitives under the hood.
- So, it turns out it’s actually possible to do asynchronous coding inside of C++ in certain cases.
- This is something that is provided by the OS itself.
    - So, the way this works is lil different than JS but roughly the same thing.
    - The idea is that we tell the OS/kernel that - i wanna go ahead & download this resource & then the kernel is actually going to manage downloading that code. It’s happening in the kernel not inside of the application. And so we can then ping the kernel if it’s done with the request.
    - Once it’s done we can call some other methods to get the results of the request.
    - Now, since this is a part of the kernel we’ve to use a different mechanism for each different OS.
        - So, it’s called
        - epoll in linux
        - kqueue in macos
        - GetQueuedCompletionStatusEx in Windows
    - So, since kernel is doing the work for us. We don’t need to assign a bg thread. (so it’s actually happening in the main thread itself) (thus we aren’t limited by the thread pool)

Event Loop (Oversimplification)

- It acts like a central dispatch for all these requests.
- Whenever we make such request in js. It does some work in js itself. But eventually it gets to the point where it’s gonna cross from js to C++. That’s when the request gets to the event loop.
- And event loop’s gonna look at this request (& again this is just an oversimplification (a lot more is done BTS)) & check
    - If this is a synchronous method. Okay so within the thread that i’m running in, i’m gonna ship off to some other (C++ code) that’s gonna go and do that request right then & there.
    - If it’s an asynchronous request, it checks
        - Is this something i can run using a C++ async primitive. If so then it’ll ship it off to the bit of C++ code that directly handles that (outside the main thread).
        - If not. Then it’s gonna have to go into a bg thread.
        - So, event loop is the one that manages it.  Whenever the call finished’s it signal the event loop (either by the thread or the C++ code (C++ async primitive)). And then it’s gonna go notify back across V8 (back into js land).
        - And then inside of js, node is going to go & call all of those callbacks that’re registered & waiting for that result.

![image](https://user-images.githubusercontent.com/66965591/176020729-673f6a17-4318-4549-a122-3086ebb9f3e1.png)

- Kernel Async
    - It’s pretty much all of our networking.
    - Network most of the time is done using KA mechanisms so we’re not limited to the subject of the thread pool.
    - Same thing with Pipes &  all of the dns.resolve calls.
- Thread Pool
    - Everything in the fs module
        - Turns out there is no C++ async primitive for file i/o
    - dns.lookup & pipes (edge cases)
- UNIX
    - UNIX domain sockets (IPC calls n things like that)
    - N ol the other remaining is handled in handled by the kernel async in the UNIX
- Windows (reverse story)
    - Child Process , TTY & some TCP server (edge cases) - Are all handles using threads - As windows doesn’t provide those primitives


# 30 June 2022 - Day 26

HTTP STATUS CODES
1. [Informational responses](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#information_responses) (`100`–`199`)
2. [Successful responses](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#successful_responses) (`200`–`299`)
3. [Redirection messages](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#redirection_messages) (`300`–`399`)
4. [Client error responses](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#client_error_responses) (`400`–`499`)
5. [Server error responses](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#server_error_responses) (`500`–`599`)

# 1 July 2022 - Day 27
Today's Progress:
- Express basic setup
- route params
- static files/assets
- json/stringify
![image](https://user-images.githubusercontent.com/66965591/176964668-775c78ef-43f6-49f8-b108-6aa78259d9dd.png)
