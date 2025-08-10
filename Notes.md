# Spring MVC Request Mapping Notes

This guide explains how to use Spring annotations for HTTP methods in REST APIs, with examples for GET, POST, PUT, PATCH, and DELETE requests.

## 📌 Common Spring Annotations

- **@Controller**: Marks a class as a Spring MVC controller.
- **@RestController**: Combines @Controller + @ResponseBody; all methods return HTTP responses directly (usually as JSON).
- **@RequestMapping**: Maps requests to controllers/classes or methods for any HTTP method. Helps define base url at class level.
- **@GetMapping**, **@PostMapping**, **@PutMapping**, **@PatchMapping**, **@DeleteMapping**: Specialized mappings for specific HTTP methods.
- **@PathVariable**: Binds a variable from the URL path.
- **@RequestParam**: Binds a variable from the query string.
- **@RequestBody**: Binds a variable from the HTTP request body.

## 🧑💻 Example Controller: Path & Query/Body Parameters

```java
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/users") // Base path for all endpoints in this controller
public class UserController {

    // Sample User model
    public static class User {
        public int id;
        public String name;
        public String role;
        public User(int id, String name, String role) { this.id = id; this.name = name; this.role = role; }
    }

    // GET: /users/{id}?role=admin
    @GetMapping("/{id}")
    public User getUser(@PathVariable int id, @RequestParam(required = false) String role) {
        return new User(id, "John Doe", role != null ? role : "user");
    }

    // POST: /users (body: JSON with name & role)
    @PostMapping
    public User createUser(@RequestBody User user) {
        // Sample logic: pretend to create and assign new id
        return new User(101, user.name, user.role);
    }

    // PUT: /users/{id} (body: JSON with name & role)
    @PutMapping("/{id}")
    public User updateUser(@PathVariable int id, @RequestBody User user) {
        // Sample logic: update user with provided info
        return new User(id, user.name, user.role);
    }

    // PATCH: /users/{id} (body: JSON with changed fields)
    @PatchMapping("/{id}")
    public User patchUser(@PathVariable int id, @RequestBody User user) {
        // Sample logic: update only changed fields
        return new User(id, user.name != null ? user.name : "John Doe", user.role != null ? user.role : "user");
    }

    // DELETE: /users/{id}?reason=duplicate
    @DeleteMapping("/{id}")
    public String deleteUser(@PathVariable int id, @RequestParam(required = false) String reason) {
        // Sample logic: pretend to delete
        return "User " + id + " deleted" + (reason != null ? " due to: " + reason : "");
    }
}
```

## 🌟 How Requests Map to Methods

| HTTP Method | URL Pattern | Handler Annotation | Path Params | Query Params | Body |
|-------------|-------------|--------------------|-------------|--------------|------|
| GET         | /users/{id}?role=admin | @GetMapping | id | role | — |
| POST        | /users      | @PostMapping | — | — | User |
| PUT         | /users/{id} | @PutMapping | id | — | User |
| PATCH       | /users/{id} | @PatchMapping | id | — | User |
| DELETE      | /users/{id}?reason=duplicate | @DeleteMapping | id | reason | — |

## 🔎 Request & Response Examples

**1. GET**
```
GET /users/42?role=admin
Response: { "id": 42, "name": "John Doe", "role": "admin" }
```

**2. POST**
```
POST /users
Body: { "name": "Alice", "role": "manager" }
Response: { "id": 101, "name": "Alice", "role": "manager" }
```

**3. PUT**
```
PUT /users/42
Body: { "name": "Jack", "role": "editor" }
Response: { "id": 42, "name": "Jack", "role": "editor" }
```

**4. PATCH**
```
PATCH /users/42
Body: { "role": "admin" }
Response: { "id": 42, "name": "John Doe", "role": "admin" }
```

**5. DELETE**
```
DELETE /users/42?reason=duplicate
Response: "User 42 deleted due to: duplicate"
```

## 📚 Summary Table: Spring MVC REST Annotations

| Annotation | Purpose |
|------------|---------|
| @Controller | Marks a class as a web controller |
| @RestController | Combines controller + direct response output |
| @RequestMapping | General-purpose URL-to-method mapping |
| @GetMapping | Handles HTTP GET requests |
| @PostMapping | Handles HTTP POST requests |
| @PutMapping | Handles HTTP PUT requests |
| @PatchMapping | Handles HTTP PATCH requests |
| @DeleteMapping | Handles HTTP DELETE requests |
| @PathVariable | Binds a variable from the URL path |
| @RequestParam | Binds a variable from the query string |
| @RequestBody | Binds data from the HTTP request body |

## ✅ Recall & Best Practices

- Use shortcut annotations (@PostMapping, etc.) instead of generic @RequestMapping(method=...) for clarity.
- Use @PathVariable for information in the URL and @RequestParam for query string values.
- @RequestBody lets your controller receive data sent as JSON or other types.
- Always document your endpoints for easy team collaboration!

---
You can copy this `README.md` file to your documentation or development resources for quick reference and team onboarding.
