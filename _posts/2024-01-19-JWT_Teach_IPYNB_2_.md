---

---

### What are JWT tokens?

- JSON Web Tokens (JWTs) are open standards (RFC 7519) for securely transmitting information between parties as JSON objects.
- They're compact, URL-safe, and self-contained, making them ideal for authentication and authorization in web APIs.
- They consist of three parts, separated by dots:
  - Header: Specifies the type of token and the algorithm used to sign it.
  - Payload: Contains the actual information being transmitted, such as user data or claims.
  - Signature: Ensures the integrity of the token and prevents tampering. It's generated using a secret key.

#### How to impelent JWT in a Flask Project:



##### 1. Install the Flask-JWT-Extended extension:


```python
pip install Flask-JWT-Extended
```

##### 2. Create Flask app and initialize JWT:


```python
from flask import Flask
from flask_jwt_extended import JWTManager

app = Flask(__name__)
app.config['JWT_SECRET_KEY'] = 'your-secret-key'  # Replace with a strong secret key
jwt = JWTManager(app)
```

##### 3. Create a login endpoint to generate tokens:


```python
@app.route('/login', methods=['POST'])
def login():
    # Verify user credentials
    if verify_credentials():  # Replace with your authentication logic
        user_id = get_user_id()
        access_token = create_access_token(identity=user_id)  # JWT creation
        return jsonify({'access_token': access_token})
    else:
        return jsonify({'error': 'Invalid credentials'}), 401
```

##### 4. Protect routes with @jwt_required decorator:


```python
@app.route('/protected')
@jwt_required
def protected():
    current_user = get_jwt_identity()  # Access user information from token
    return jsonify({'message': 'Hello, {}!'.format(current_user)})

```

**VALIDATION**


Validating a JWT (JSON Web Token) takes multiple steps. Below is a simple Python script using the PyJWT library to demonstrate JWT validation. 

Make sure to install the library first 


```python
pip install PyJWT
pip3 for macbook
```

After that, run this python script using the PyJWT library to demonstrate JWT validation


```python
import jwt
from datetime import datetime, timedelta

# Your secret key for JWT validation
SECRET_KEY = 'your_secret_key_here'
# What the code above does is import the jwt module(which is apart of the PyJWT library,) 
# We also import datetime and timedelta from the standard python library
# Then finally set a secret key variable, which is used to encode and decode the JWT

def create_jwt():
    # Create a sample JWT for demonstration purposes
    payload = {
        'user_id': 123,
        'username': 'john_doe',
        'exp': datetime.utcnow() + timedelta(hours=1)  # Token expiration time
    }
    token = jwt.encode(payload, SECRET_KEY, algorithm='HS256')
    return token
# The create_jwt function generates a sample JWT
# It creates a payload with a user ID, username, and an expiration time (exp) set to one hour from the current UTC time. 
# The payload is then encoded using the jwt.encode function, and the resulting token is returned.
def validate_jwt(token):
    try:
        # Decode and verify the JWT
        payload = jwt.decode(token, SECRET_KEY, algorithms=['HS256'])
        print("JWT Validation Successful!")
        print("Payload:", payload)
    except jwt.ExpiredSignatureError:
        print("JWT has expired. Please obtain a new token.")
    except jwt.InvalidTokenError:
        print("Invalid JWT. Authentication failed.")
# The validate_jwt function takes a JWT token as input and tries to decode and verify it
# If the validation is successful, it prints a success message + the decoded payload.
# If the token has expired, it catches the ExpiredSignatureError and prints a message about token expiration
# If the token is invalid for other reasons, it catches the InvalidTokenError and prints a message about authentication failure.
if __name__ == "__main__":
    # Step 1: Create a JWT
    jwt_token = create_jwt()
    print("Generated JWT:", jwt_token)

    # Step 2: Validate the JWT
    validate_jwt(jwt_token)

# The __main__ block demonstrates the usage of the script. It first creates a JWT using the create_jwt function and prints the generated JWT
# Then validates the JWT using the validate_jwt function.
# he output will show the success message or specific error messages based on the validation result.

```

    Generated JWT: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyX2lkIjoxMjMsInVzZXJuYW1lIjoiam9obl9kb2UiLCJleHAiOjE3MDU2OTU5MzV9.Kw_fOaEHQTlrt-XqIqiMzZFGaBncX9_Bl8GVNFItRhc
    JWT Validation Successful!
    Payload: {'user_id': 123, 'username': 'john_doe', 'exp': 1705695935}


**What this does is:**

-Creates a JWT with a sample payload.

-Prints the generated JWT.

-Validates the JWT and prints the payload if the validation is successful.

** Replace 'your_secret_key_here' with your actual secret key. This script uses the HS256 algorithm for HMAC with SHA-256, but you can choose a different algorithm based on different requirements.



## Postman Introduction:

Postman is a tool that helps applications communicate over the internet by making it easy to send and receive messages (requests and responses).
It's like a friendly messenger ensuring smooth conversations between different software, making it essential for testing and debugging during app development.
Functionality:

Postman allows developers to test APIs, ensuring that services work as expected by sending and receiving requests in a user-friendly interface.
It also helps in checking and managing cookies, crucial for apps to remember information during their interactions with servers.


## Example of a piece of code



```python
// Postman Test Script
pm.test("Response Status is 200", function () {
    pm.response.to.have.status(200);
});
```

In Postman, this script is like an automated check to make sure that when you ask a server for something (like data from an API), the server responds with a "200 OK" message, which means everything went well. If the response isn't a "200 OK," the script lets you know that something might be wrong, helping you catch issues when testing your application. It's a way to quickly see if the server is behaving as expected.

![Screenshot 2024-01-19 at 11.23.44 AM.png](<Screenshot 2024-01-19 at 11.23.44 AM.png>)
