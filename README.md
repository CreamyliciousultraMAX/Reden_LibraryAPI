# 📖🔗 LIBRARY API  

A robust backend service designed to efficiently manage library resources. This project is ideal for developers building library management systems or similar applications.  

---

## 📚 Project Overview  

The **Library API** provides secure and flexible endpoints to manage books, authors, users, and borrowing records, all while leveraging JSON Web Token (JWT) authentication for secure access.  

---

## ✨ Features  

- **🔒 JWT Authentication**: Ensures secure access using JSON Web Tokens.  
- **🚫 Token Revocation**: Tokens are invalidated after single use for enhanced security.  
- **🛠️ CRUD Operations**: Seamless management of books, authors, users, and relationships.  
- **⚠️ Error Handling**: Comprehensive error messages for debugging and client guidance.  

---

## 🔧 Technologies  

- **🐘 PHP**: Core logic implemented using PHP.  
- **🎯 Slim Framework**: Lightweight and flexible PHP framework.  
- **🔥 Firebase JWT**: Manages token generation and validation.  
- **📜 PSR-7**: Standardized HTTP message interfaces.  

---

## 🔑 Authentication  

### 🔍 **Overview**  
The Library API uses **JWT** for secure authentication.  

1. Clients include a token in the `Authorization` header of API requests.  
2. Tokens are validated and revoked after one use.  
3. Revoked tokens are tracked via PHP sessions for additional security.  

### 🌀 **Token Workflow**  

- **🎟️ Token Generation**: After successful login.  
- **✅ Validation**: Middleware ensures tokens are valid and unexpired.  
- **🚫 Revocation**: Tokens are invalidated upon use. 

## 🛠️ CRUD OPERATIONS 
**🎟️ Token Generation**: After successful login.  
- **✅ Validation**: Middleware ensures tokens are valid and unexpired.  
- **🚫 Revocation**: Tokens are invalidated upon use.

#
# 👤 **User Side** 
## USER REGISTER
-  **Endpoint**:  `user/register`
-  **Method**: `POST`
-  **Description**: User can input their username and password to create an account that will be saved on the database. 

### 📥 Sample JSON request:
```bash
  {
    "username": "Super",
    "password": "Mario"
  }
```
-  **Response:**

    - **On Success**
    ```bash
      {
        "status": "success",
        "data": null
      }
    ```

    - **On Error (Account Duplication)**
    ```bash
      {
        "status": "fail",
        "data": {
          "title": "Username already exists"
        }
      }
    ```
#
## USER LOGIN
-  **Endpoint**:  `user/login`
-  **Method**: `POST`
-  **Description**: User can input their username and password to access their created account based on their ceredentials saved on the database to create a session. 

### 📥 Sample JSON request:
```bash
  {
    "username": "Super",
    "password": "Mario"
  }
```
-  **Response:**

    - **On Success**
    ```bash
      {
        "status": "success",
        "data": {
          "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9. 
        }
      }
    ```

    - **On Error**
    ```bash
      {
        "status": "fail",
        "data": {
          "title": "Invalid credentials"
        }
      }
    ```
#
## USER AUTHENTICATE
-  **Endpoint**:  `user/confirmation`
-  **Method**: `POST`
-  **Description**: After the login of users, their credentials will be authenticated for them to access different functionalities.

### 📥 Sample JSON request:
```bash
  {
    "username": "Super",
    "password": "Mario"
  }
```
-  **Response:**

    - **On Success**
    ```bash
      {
        "status": "success",
        "data": {
          "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.
        }
      }
    ```

    - **On Error**
    ```bash
      {
        "status": "fail",
        "data": {
          "title": "Authentication failed"
        }
      }
    ```

#
## USER VIEWING OF ACCOUNT
-  **Endpoint**:  `user/account`
-  **Method**: `POST`
-  **Description**: The user can view their own account with their username and password that is hased using SHA256, but it will require them a token  from authentication.

### 📥 Sample JSON request:
```bash
      {
          "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9"
      }
```
-  **Response:**

    - **On Success**
    ```bash
      {
        "status": "success",
        "data": {
          "username": "Super",
          "password": "61c8e16ad90d4e6da317180fa445e262e9313bbf21fd4d30b3b9b4425886b2f5"
        }
      }
    ```

    - **On Error (Token Expired or Invalid Token)**
    ```bash
      {
        "status": "fail",
        "data": {
          "title": "Token invalid or expired"
        }
      }
    ```
#
# AUTHOR SIDE
## AUTHOR REGISTER
-  **Endpoint**:  `author/register`
-  **Method**: `POST`
-  **Description**: Authors can input their username and password to create an account that will be saved on the database. 

### 📥 Sample JSON request:
```bash
  {
    "username": "Son",
    "password": "Goku"
  }
```
-  **Response:**

    - **On Success**
    ```bash
      {
        "status": "Author Registered Successfully",
        "data": null
      }
    ```

    - **On Error (Account Duplication)**
    ```bash
      {
        "status": "fail",
        "data": {
          "title": "Author name already exists"
        }
      }
    ```
#
## AUTHOR LOGIN
-  **Endpoint**:  `author/login`
-  **Method**: `POST`
-  **Description**: Author can login their own account based on their regestration credentials that is saved on the database.

### 📥 Sample JSON request:
```bash
  {
    "username": "Son",
    "password": "Goku"
  }
```
-  **Response:**

    - **On Success**
    ```bash
      {
        "status": "Author Log In Successfully",
        "data": {
          "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.
        }
      }
    ```

    - **On Error (Account Duplication)**
    ```bash
      {
        "status": "fail",
        "data": {
          "title": "Authors credential is invalid"
        }
      }
    ```
#
## AUTHOR CONFIRMATION
-  **Endpoint**:  `author/confirmation`
-  **Method**: `POST`
-  **Description**: After the login of Authors, their credentials will be authenticated for them to access different functionalities.

### 📥 Sample JSON request:
```bash
  {
    "username": "Son",
    "password": "Goku"
  }
```
-  **Response:**

    - **On Success**
    ```bash
      {
        "status": "Author Authenticated",
        "data": {
          "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9"
        }
      }
    ```

    - **On Error (Token Expired or Invalid Token)**
    ```bash
      {
        "status": "fail",
        "data": {
          "title": "Author Authentication failed"
        }
      }
    ```
#
## AUTHOR POSTING OF BOOKS
-  **Endpoint**:  `author/posting`
-  **Method**: `POST`
-  **Description**: After the author got authenticated the author can publish their own books and add their own title for their books.

### 📥 Sample JSON request:
```bash
{
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9",
    "title": "Dragon Ball Z"
}
```
-  **Response:**

    - **On Success**
    ```bash
      {
        "status": "success",
        "data": {
          "message": "Book posted successfully"
        }
      }
    ```

    - **On Error (Token Expired or Invalid Token)**
    ```bash
      {
        "status": "fail",
        "data": {
          "title": "Invalid or expired token"
        }
      }
    ```
## AUTHOR DELETION OF BOOKS
-  **Endpoint**:  `books/delete`
-  **Method**: `DELETE`
-  **Description**: With proper authentication the author can delete their own books they posted.

### 📥 Sample JSON request:
```bash
  {
      "bookid": 28,
      "token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9"
  }
```
-  **Response:**

    - **On Success**
    ```bash
    {
      "status": "success",
      "data": {
        "title": "Book deleted successfully"
      }
    }
    ```

    - **On Error (Token Expired or Invalid Token)**
    ```bash
    {
      "status": "fail",
      "data": {
        "title": "Invalid token, access denied"
      }
    }
    ```
    ```bash
    {
      "status": "fail",
      "data": {
        "title": "Author not found"
      }
    }
    ```
    ```bash
    {
      "status": "fail",
      "data": {
        "title": "Book not found or you do not have permission to delete this book"
      }
    }
    ```
# GENERAL ACCESS FOR AUTHORS AND USERS
## BOTH AUTHOR AND USERS CAN VIEW BOOKS
-  **Endpoint**:  `books/viewbooks`
-  **Method**: `POST`
-  **Description**: With proper authentication the users and authors can view the books being posted by the authors or other authors

### 📥 Sample JSON request:
```bash
    {
        "token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9"
    }

```
-  **Response:**

    - **On Success**
    ```bash
    {
      "status": "success",
      "data": [
        {
          "bookid": 30,
          "title": "Dragon Ball Z"
        }
      ]
    }
    ```

    - **On Error (Token Expired or Invalid Token)**
    ```bash
    {
      "status": "fail",
      "data": {
        "title": "Token invalid or expired"
      }
    }
    ```
## BOTH AUTHOR AND USERS CAN VIEW AUTHORS
-  **Endpoint**:  `author/viewauthors`
-  **Method**: `POST`
-  **Description**: With proper authentication the users and authors can view Authors or Athors can view other Authors that has created an account.

### 📥 Sample JSON request:
```bash
  {
      "token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9"
  }
```
-  **Response:**

    - **On Success**
    ```bash
    {
      "status": "success",
      "data": [
        {
          "authorid": 17,
          "username": "dannah"
        },
        {
          "authorid": 18,
          "username": "dani"
        },
        {
          "authorid": 19,
          "username": "Son"
        }
      ]
    }
    ```

    - **On Error (Token Expired or Invalid Token)**
    ```bash
    {
      "status": "fail",
      "data": {
        "title": "Token invalid or expired"
      }
    }
    ```
## BOTH AUTHOR AND USERS CAN VIEW AUTHORS AND BOOKS
-  **Endpoint**:  `book/author/view`
-  **Method**: `POST`
-  **Description**: With proper authentication the users and authors can view Authors and the books that they posted.

### 📥 Sample JSON request:
```bash
  {
      "authorid" : 19,
      "bookid": 30,
      "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9"
  } 

```
-  **Response:**

    - **On Success**
    ```bash
    {
      "status": "success",
      "data": {
        "author": {
          "id": 19,
          "username": "Son"
        },
        "book": {
          "id": 30,
          "title": "Dragon Ball Z"
        }
      }
    }
    ```

    - **On Error (Token Expired or Invalid Token)**
    ```bash
    {
      "status": "fail",
      "message": "Author or Book not found"
    }
    ```
    ```bash
    {
      "status": "fail",
      "message": "Invalid token, access denied"
    }
    ```
    ```bash
  {
    "status": "fail",
    "message": "Connection failed: Expired token"
  }
    ```
