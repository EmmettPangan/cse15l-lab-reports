# Lab Report 2
By: Emmett Pangan

## Part 1: StringServer
```
import java.io.IOException;
import java.io.OutputStream;
import java.net.InetSocketAddress;
import java.net.URI;

import com.sun.net.httpserver.HttpExchange;
import com.sun.net.httpserver.HttpHandler;
import com.sun.net.httpserver.HttpServer;

interface URLHandler {
    String handleRequest(URI url);
}

class StringHandler implements URLHandler {

    String runningString = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return runningString;
        } else if (url.getPath().equals("/add-message")) {
            String[] parameters = url.getQuery().split("=");
            if (parameters[0].equals("s")) {
                runningString += parameters[1] + "\n";
                return runningString;
            }
        }
        return "404 Error";
    }
}

class ServerHttpHandler implements HttpHandler {
    URLHandler handler;

    ServerHttpHandler(URLHandler handler) {
      this.handler = handler;
    }

    public void handle(final HttpExchange exchange) throws IOException {
        // form return body after being handled by program
        try {
            String ret = handler.handleRequest(exchange.getRequestURI());
            // form the return string and write it on the browser
            exchange.sendResponseHeaders(200, ret.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(ret.getBytes());
            os.close();
        } catch(Exception e) {
            String response = e.toString();
            exchange.sendResponseHeaders(500, response.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(response.getBytes());
            os.close();
        }
    }
}

public class StringServer {
    public static void start(int port, URLHandler handler) throws IOException {
        HttpServer server = HttpServer.create(new InetSocketAddress(port), 0);

        //create request entrypoint
        server.createContext("/", new ServerHttpHandler(handler));

        //start the server
        server.start();
        System.out.println("Server Started! Visit http://localhost:" + port + " to visit.");
    }

    public static void main(String[] args) throws IOException {
        StringServer.start(Integer.parseInt(args[0]), new StringHandler());
    }
}
```

When any URL is requested, the ``handleRequest`` method in the ServerHttpHandler class is called in order to determine what to display to the user. The URI ``url`` parameter in the ``handleRequest`` method is given the URL that is requested. In this case, ``url`` gets a URI object that corresponds to the ``/add-message?s=Hello`` path. The ``handleRequest`` method checks for a valid URL path, that is, one which includes ``/add-message``. Next, after passing the check, the query component of the URL is obtained using ``getQuery`` on ``url``, split up into the keys and values for the given queries. Since we only want to add a message when the query key is ``s``, ``handleRequest`` checks the query key, and if it matches ``s``, then it concatenates its value to the ``runningString`` variable along with a new line. In this case, the value that is concatenated is the String "Hello". ``runningString`` is returned to be displayed to the user.

<img width="337" alt="image" src="https://user-images.githubusercontent.com/110417473/215021168-0ac51311-e56a-4226-9000-147d6400f14d.png">

<img width="395" alt="image" src="https://user-images.githubusercontent.com/110417473/215021232-677e3c2c-a488-407a-a249-140ff965346a.png">
