# EX01 Developing a Simple Webserver
## Date:26/11/26

## AIM:
To develop a simple webserver to serve html pages and display the Windows Specifications of your Laptop.

## DESIGN STEPS:
### Step 1: 
HTML content creation.

### Step 2:
Design of webserver workflow.

### Step 3:
Implementation using Python code.

### Step 4:
Import the necessary modules.

### Step 5:
Define a custom request handler.

### Step 6:
Start an HTTP server on a specific port.

### Step 7:
Run the Python script to serve web pages.

### Step 8:
Serve the HTML pages.

### Step 9:
Start the server script and check for errors.

### Step 10:
Open a browser and navigate to http://127.0.0.1:8000 (or the assigned port).

## PROGRAM:
```

from http.server import HTTPServer, SimpleHTTPRequestHandler
from pathlib import Path
from html import escape

HOST = "127.0.0.1"
PORT = 8000

# Enter your details here
STUDENT_NAME = "tonesh"
REGISTER_NUMBER = "26009529"


class MyHandler(SimpleHTTPRequestHandler):

    def __init__(self, *args, **kwargs):
        super().__init__(
            *args,
            directory=str(Path(__file__).parent),
            **kwargs
        )

    def do_GET(self):

        if self.path in ("/", "/index.html"):

            file_path = Path(__file__).parent / "index.html"

            if not file_path.exists():
                self.send_error(404, "index.html not found")
                return

            page = file_path.read_text(encoding="utf-8")

            student_details = f"""
            <hr>
            <h3>Student Details</h3>
            <p>Name: {escape(STUDENT_NAME)}</p>
            <p>Register Number: {escape(REGISTER_NUMBER)}</p>
            """

            page = page.replace(
                "</body>",
                student_details + "</body>"
            )

            data = page.encode("utf-8")

            self.send_response(200)
            self.send_header(
                "Content-Type", "text/html; charset=utf-8"
            )
            self.send_header("Content-Length", str(len(data)))
            self.end_headers()

            self.wfile.write(data)

        else:
            super().do_GET()


if __name__ == "__main__":

    server = HTTPServer((HOST, PORT), MyHandler)

    print("Web Server Started Successfully!")
    print("Open: http://127.0.0.1:8000")

    try:
        server.serve_forever()
    except KeyboardInterrupt:
        print("\nServer stopped.")
        server.server_close()

```
## OUTPUT:
<img width="1912" height="970" alt="Screenshot 2026-11-25 212958" src="https://github.com/user-attachments/assets/edb1827f-14b3-4a90-a6d9-36ea33c95746" />


## RESULT:
The program for implementing simple webserver is executed successfully.
