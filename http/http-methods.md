## 🔍 Safe Methods — No Side Effects

* **GET**
    * → **Retrieve a resource.** Should only fetch data, never modify it. Idempotent and cacheable. Use for reading data.

* **HEAD**
    * → **Get response headers only.** Same as GET but without the response body. Useful for checking resource existence or metadata without downloading content.

* **OPTIONS**
    * → **Get allowed methods for a resource.** Returns the HTTP methods that the server supports for the target resource. Used for CORS preflight requests.


## ✏️ Methods That Modify State

* **POST**
    * → **Create a new resource or submit data.** Not idempotent—multiple identical requests may create multiple resources. Use for creating resources or submitting forms.

* **PUT**
    * → **Replace a resource entirely.** Idempotent—multiple identical requests have the same effect as one. Creates the resource if it doesn't exist, replaces it if it does.

* **PATCH**
    * → **Partially update a resource.** Modifies only specified fields. Should be idempotent when possible. Use for partial updates instead of PUT.

* **DELETE**
    * → **Remove a resource.** Idempotent—deleting an already-deleted resource has no effect. Use for removing resources.


## 🔧 Other Methods

* **CONNECT**
    * → **Establish a tunnel to the server.** Used for HTTPS tunneling through proxies. Converts the connection to a TCP/IP tunnel.

* **TRACE**
    * → **Echo the received request.** Returns the request as received by the server. Useful for debugging but often disabled for security reasons.


## 📊 Method Characteristics

| Method | Idempotent | Safe | Cacheable | Request Body | Response Body |
|--------|------------|------|-----------|--------------|---------------|
| GET    | ✅ Yes     | ✅ Yes | ✅ Yes    | ❌ No        | ✅ Yes        |
| HEAD   | ✅ Yes     | ✅ Yes | ✅ Yes    | ❌ No        | ❌ No         |
| POST   | ❌ No      | ❌ No | ⚠️ Conditional | ✅ Yes | ✅ Yes        |
| PUT    | ✅ Yes     | ❌ No | ❌ No     | ✅ Yes        | ✅ Yes        |
| PATCH  | ⚠️ Should be | ❌ No | ❌ No     | ✅ Yes        | ✅ Yes        |
| DELETE | ✅ Yes     | ❌ No | ❌ No     | ⚠️ Optional   | ✅ Yes        |
| OPTIONS| ✅ Yes     | ✅ Yes | ❌ No     | ❌ No        | ✅ Yes        |
| CONNECT| ❌ No      | ❌ No | ❌ No     | ❌ No        | ✅ Yes        |
| TRACE  | ✅ Yes     | ✅ Yes | ❌ No     | ❌ No        | ✅ Yes        |


## 💡 Common Use Cases

* **GET** → Fetching user profiles, listing items, retrieving data
* **POST** → Creating new users, submitting forms, file uploads
* **PUT** → Replacing entire user profiles, updating complete resources
* **PATCH** → Updating user email, modifying specific fields
* **DELETE** → Removing users, deleting posts, cleaning up resources
* **HEAD** → Checking if a file exists, validating ETags, pre-flight checks
* **OPTIONS** → CORS preflight requests, discovering API capabilities

