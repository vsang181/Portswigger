# What is the difference between authentication and authorization?

Although they work closely together, **authentication** and **authorization** serve two distinct security purposes in an application.

## Key Differences

| **Feature** | **Authentication** | **Authorization** |
| -------- | ------- | ------- |
| **Core Question** | _"Who are you?"_ | _"What are you allowed to do?"_ |
| **Purpose** | Verifies that a user is genuinely who they claim to be. | Verifies whether an authenticated user has permission to perform an action or access a resource. |
| **Timing** | Happens first (e.g., during login). | Happens second, after the user's identity is confirmed. |

## Practical Example

- **Authentication**: When someone logs in with the username `Carlos123`, authentication checks their credentials to confirm they are the actual owner of that account.

- **Authorization**: Once `Carlos123` is logged in, authorization checks their account permissions to decide what they can do next such as viewing other users' personal data or deleting another user's account.
