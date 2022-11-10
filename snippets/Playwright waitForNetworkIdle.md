In playwright the `page.waitForNetworkIdle` method doesn't actually wait for network idle. the promise has a max idle time of `500ms` only. It's a boomer as if you have multiple request dependencies in your app or some request that naturally takes more time to load, it won't wait for that. Last week when I was working on our test suite I had this axact issue. After a lot of github issue browsing, I wrote a small function that by default waits for `1` second and has the flexibility to wait `indefinitely` untill the network is `actually` idle. Here is it
```ts
/**

* wait for network idle (by default this will resolve after `a second` if there are no requests pending)

* @param idlePeriod - time in ms to wait for no requests, set to `-1` to wait indefinitely

* @default 1000

*/

export async function waitForNetworkIdle(page: Page, idlePeriod = 1000) {

return await new Promise(resolve => {

// eslint-disable-next-line prefer-const

let timeout: NodeJS.Timeout

// maintain a counter of the number of requests

// this is an array to keep track of request-response pairs,

// so that we can ignore requests that have already been responded to

let reqStack: string[] = []

// we need this flag so that orphan responses

// don't resolve the promise

let startedWaiting = false

  

const onRequest = (req: Request) => {

if (!startedWaiting) startedWaiting = true

  

reqStack.push(req.url())

}

  

const onResponse = (req: Request) => {

// wait for request to be added to the stack

if (!startedWaiting) return

  

// this promise will resolve when the page has a response

// or on the next tick

const pageTick = page.evaluate(async () => {

return await new Promise(resolve => setTimeout(resolve, 0))

})

  

// eslint-disable-next-line no-void

void pageTick

.catch(() => null)

.then(() => {

// check if the response is in the stack and remove it

if (reqStack.includes(req.url())) {

reqStack = reqStack.filter(url => url !== req.url())

}

  

// if the stack is empty, it means there are no more requests

// we can resolve the promise

if (reqStack.length === 0) {

removeListenersAndResolve()

  

if (timeout !== undefined) clearTimeout(timeout)

}

})

}

  

const removeListenersAndResolve = () => {

page.removeListener('request', onRequest)

// spell-checker: disable

page.removeListener('requestfinished', onResponse)

page.removeListener('requestfailed', onResponse)

// spell-checker: disable

  

resolve(null)

}

  

// when we have an idle period, we can set a timeout

// so that the promise resolves even if there are requests

// after the idle period

if (idlePeriod !== -1) {

timeout = setTimeout(removeListenersAndResolve, idlePeriod)

}

  

page.addListener('request', onRequest)

// spell-checker: disable

page.addListener('requestfinished', onResponse)

page.addListener('requestfailed', onResponse)

// spell-checker: disable

})

}
```