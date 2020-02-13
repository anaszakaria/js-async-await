## js-async-await
### Short notes on Javascript Async Await

#### Async Return Promise
```
async function getMessage() {
    return 'Fetching Data'
}

getMessage().then(msg => console.log('Message:', msg))
```

#### Return Await
```
async function getUsers() {
    const response = await axios.get('https://jsonplaceholder.typicode.com/users')
    return response.data
}

getUsers().then(users => console.log('Users:', users))
```

#### Return Await .then()
```
async function getComment(postID) {
    return await axios.get(`https://jsonplaceholder.typicode.com/comments?postId=${postID}`)
    .then(response => response.data)
}

getComment(1).then(data => console.log(`Post 1 Comments:`, data))
```

#### Return Await .then().catch()
```
async function getAllPost() {
    return await axios.get('https://jsonplaceholder.typicode.com/posts')
    .then(response => {
        return response.data
    })
    .catch(error => {
        console.log(error)
    })
}

getAllPost().then(posts => console.log('All Posts:', posts))
```

#### Error Handling
```
async function getTodos() {
    try {
        const response = await axios.get('https://jsonplaceholder.typicode.com/todos')
        return response.data
    } catch(error) {
        console.log('error', error)
    }
}

getTodos().then(todos => console.log('To Do List:', todos))
```

#### Error Handling Multiple Requests
```
async function getSelectedUsers() {
    try {
        const user1 = await axios.get('https://jsonplaceholder.typicode.com/users/1')
        const user2 = await axios.get('https://jsonplaceholder.typicode.com/users/2')
        const user3 = await axios.get('https://jsonplaceholder.typicode.com/users/3')
        return [user1.data, user2.data, user3.data]
    } catch (error) {
        return error
    }
}

getSelectedUsers()
.then(user => console.log('Selected User:', user))
.catch(error => console.log(error))
```

#### Promise All
```
async function promiseGetSelectedUsers() {
    const response = await Promise.all([
        axios.get('https://jsonplaceholder.typicode.com/users/1'),
        axios.get('https://jsonplaceholder.typicode.com/users/2'),
        axios.get('https://jsonplaceholder.typicode.com/users/3')
    ])
    const userData = response.map(user => user.data)
    console.log('Promise All:', userData)
}

promiseGetSelectedUsers()
```

#### Async Await Multiple Requests without Promise All
```
async function getPost() {
    const user = await axios.get('https://jsonplaceholder.typicode.com/users/1')
    const post = await axios.get('https://jsonplaceholder.typicode.com/posts?userId=1')
    return { user, post }
}

getPost().then(result => console.log('User and Posts:', result))
```

#### Queue Async Await
```
async function getDataInSequence() {
    const posts = await axios.get('https://jsonplaceholder.typicode.com/posts')
    console.log('Posts', posts)
    const comments = await axios.get('https://jsonplaceholder.typicode.com/comments')
    console.log('Comments', comments)
    const albums = await axios.get('https://jsonplaceholder.typicode.com/albums')
    console.log('Albums', albums)
    const photos = await axios.get('https://jsonplaceholder.typicode.com/photos')
    console.log('Photos', photos)
    const todos = await axios.get('https://jsonplaceholder.typicode.com/todos')
    console.log('Todos', todos)
    const users = await axios.get('https://jsonplaceholder.typicode.com/users')
    console.log('Users', users)
}

getDataInSequence()
```

#### Queue Async Await with setTimeout()

```
async function delay(ms) {
    return new Promise(resolve => {
        setTimeout(resolve, ms)
    })
}

async function timeOutInSequence() {
    await delay(3000)
    console.log('After 3 seconds')
    await delay(2000)
    console.log('After 5 seconds')
    await delay(1000)
    console.log('After 6 seconds')
}

timeOutInSequence()
```
