<table>
<thead>
<tr><th> Code </th><th>Description</th></tr>
</thead>
<tbody>
<tr><td> gen-1  </td><td> Follow best practices of the language</td></tr>
<tr><td> gen-2  </td><td> camelCase naming for variables</td></tr>
<tr><td> gen-3  </td><td> Uppercase constants and static</td></tr>
<tr><td> gen-4  </td><td> Capitalize first word for classes</td></tr>
<tr><td> gen-5  </td><td> Avoid global variables, use the least exposure possible</td></tr>
<tr><td> gen-6  </td><td> Avoid public variables for classes. Enforce the idea of encapsulation with getters and setter</td></tr>
<tr><td> gen-7  </td><td> Avoid redundant labeling

```javascript
//avoid:
const bookPage = book.getBookPage(1)
```
 
```javascript
//embrace:
const page = book.getPage(1)
```

</td></tr>
<tr><td> gen-8  </td><td> Use meaning full names 

```javascript
//avoid:
function calculate(a, b, c) {
    return (a * b) * c;
}
```
 
```javascript
//embrace:
function calculate(speed, distance, time) {
    return (speed * distance) * time;
}
```

<tr><td> gen-9  </td><td> Avoid constructors with more than 4 arguments, consider a builder or data object
    
```javascript
//avoid:
const book = new Book("Design Patterns Explained", "Alan Shalloway", 
                        "978-0321247148", 4.9, 480, "October 12, 2004", "English")
```
 
```javascript
//embrace:
const book = new BookBuilder.setTitle("Design Patterns Explained")
                .setAuthor("Alan Shalloway")
                .setISBN("978-0321247148")
                .setRating(4.9)
                .setPageCount(480)
                .setPublishDate("October 12, 2004")
                .setLanguange("English")
                .build()
```
    
</td></tr>
<tr><td> gen-10 </td><td> Consider static factory methods instead of constructors

```javascript
const location = Location.from("Buffalo", "NY")
const prime = Lists.of(2, 3, 5)
```

</td></tr>
<tr><td> gen-11 </td><td> Enforce singleton property with a private constructor or an enum type</td></tr>
<tr><td> gen-12 </td><td> Don't comment out code, just remove it</td></tr>
<tr><td> gen-13 </td><td> Obey the general contract when overriding equals and hashCode</td></tr>
<tr><td> gen-14 </td><td> Minimize mutability, use `final` or `const` judiciously</td></tr>
<tr><td> gen-15 </td><td> Design for inheritance or prohibit it (`final` or `sealed` class)</td></tr>
<tr><td> gen-16 </td><td> Replace anonymous constants with descriptive constants <br/>

```javascript
//avoid:
function isOk(response) {
    if ( anyNulls(response, response.get('code') ) return false;
    return response.get('code') === 1 // anonymous constant
}
```

```javascript
//embrace:
const OK_RESPONSE_CODE = 1 
function isOk(response) {
    if ( anyNulls(response, response.get('code') ) return false;
    return response.get('code') === OK_RESPONSE_CODE // descriptive constant
}
```

</td></tr>
<tr><td> gen-17 </td><td> Use `static final` for repetitive string constants</td></tr>
<tr><td> gen-18 </td><td> Remove unused functions</td></tr>
<tr><td> gen-19 </td><td> Avoid console output, use a logger
 
```javascript
//avoid:
function calculate(speed, distance, time) {
    console.log("calling calculate")
    /* debugger
    console.log("speed", speed)
    console.log("distance", distance)
    console.log("time", time)
    */
    // console.log("done")
    return (speed * distance) * time;
}
```
 
```javascript
//embrace:
function calculate(speed, distance, time) {
    Logger.debug("calling calculate speed:%s, distance:%s, time:%s", speed, distance, time)
    return (speed * distance) * time;
}
``` 
 
</td></tr>
<tr><td> gen-20 </td><td> Validate inputs early to avoid unintended consequences
 
 
```javascript
//avoid:
function search(user, query, limit) {
   if ( limit > MAX_RESULT ) throw new Error('limit too large')
   
   const results = searchService.query(query, limit)
   
   if ( user == null ) throw new Error('no user provided')
   else results.set('user', user)
  
   return results
}
```

```javascript
//embrace:
function search(user, query, limit) {
   if ( limit > MAX_RESULT ) throw new Error('limit too large')
   if ( user == null ) throw new Error('no user provided')
   
   const results = searchService.query(query, limit)   
   results.set('user', user)
  
   return results
}
```

 
 
 
 </td></tr>
<tr><td> gen-21 </td><td> Embrace dependency injection when available</td></tr>
<tr><td> gen-22 </td><td> Favor iterators when dealing with large collections</td></tr>
<tr><td> gen-23 </td><td> Avoid loading unnecessary items into collections for later filtering <br/>

```javascript
//avoid:
function getUser(username) {
   const allUsers = sql.getRows("SELECT id, username FORM users")
   return allUsers.find( (i) => i.username === username )
}
```

```javascript
//embrace:
function getUser(username) {
   return sql.getRows("SELECT id, username FORM users WHERE username = :username", username)
}
```

</td></tr>
<tr><td> gen-24 </td><td> Don't ignore exceptions <br/>

```javascript
//avoid:
function print(a) {
   try { return Printer.print(a) } 
   catch (e) { 
    /* something bad happend */ 
    return; 
   }
}
```

```javascript
//embrace:
function print(a) {
   try { return Printer.print(a) } 
   catch (e) { 
    handleError(e);
   }
}
```

</td></tr>
<tr><td> gen-23 </td><td> Limit number of conditionals in one function to no more than 10 (if and switch)</td></tr>
<tr><td> gen-24 </td><td> Store timestamps as UTC </td></tr>
</tbody>
</table>
