# Lab Report 2
By: Emmett Pangan

## Part 1: StringServer
### The StringServer.java File
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

### Examples
When any URL is requested, the ``handleRequest`` method in the ServerHttpHandler class is called in order to determine what to display to the user. The URI ``url`` parameter in the ``handleRequest`` method is given the URL that is requested. In this case, ``url`` gets a URI object that corresponds to the ``/add-message?s=Hello`` path. The ``handleRequest`` method checks for a valid URL path, that is, one which includes ``/add-message``. Next, after passing the check, the query component of the URL is obtained using ``getQuery`` on ``url``, split up into the key and value parameters for the given queries. Since we only want to add a message when the query key is ``s``, ``handleRequest`` checks the query key, and if it matches ``s``, then it concatenates its value to the ``runningString`` variable along with a new line. In this case, the value that is concatenated is the string "Hello". ``runningString``, which at this point only contains ``"Hello \n"``, is returned to the ``handle`` method to be displayed to the user.

<img width="337" alt="image" src="https://user-images.githubusercontent.com/110417473/215021168-0ac51311-e56a-4226-9000-147d6400f14d.png">

When the second URL is requested, the ``handleRequest`` method is called again. This time, the ``url`` parameter gets a URI object that corresponds to the ``/add-message?s=How are you`` path. Again, the method checks for a valid ``/add-message`` path and splits the query into its keys and values. Since the query key once again matches ``s``, the value of ``"How are you"`` is concatenated to the ``runningString`` variable, which now contains ``"Hello \n How are you \n"``. This string is sent back to the ``handle`` method to be displayed to the user.

<img width="395" alt="image" src="https://user-images.githubusercontent.com/110417473/215021232-677e3c2c-a488-407a-a249-140ff965346a.png">

## Part 2: Debugging
### The ``filter`` Method Before
```
static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
        if(sc.checkString(s)) {
            result.add(0, s);
        }
    }
    return result;
}
```

### Failure-Inducing Input
```
@Test
public void testFilterFail() {
    List<String> input =
            new ArrayList<>(Arrays.asList("hi", "sup", "hello", "howdy"));
    StringChecker hGreeting = new StringChecker() {
        @Override
        public boolean checkString(String s) {
            if (s.contains("h")) {
                return true;
            }
            return false;
        }
    };
    assertEquals(new ArrayList<String>(Arrays.asList("hi", "hello", "howdy")),
            ListExamples.filter(input, hGreeting));
}
```

### Passing Input
```
@Test
public void testFilterPass() {
    List<String> input =
            new ArrayList<>(Arrays.asList("hi", "sup", "hello", "hi"));
    StringChecker hGreeting = new StringChecker() {
        @Override
        public boolean checkString(String s) {
            if (s.contains("h")) {
                return true;
            }
            return false;
        }
    };
    assertEquals(new ArrayList<String>(Arrays.asList("hi", "hello", "hi")),
            ListExamples.filter(input, hGreeting));
}
```

### Symptom
<img width="543" alt="image" src="https://user-images.githubusercontent.com/110417473/215375167-84ba6478-21f0-4e8b-b18d-d620fc28c3e2.png">

### The ``filter`` Method After
```
static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
        if(sc.checkString(s)) {
            result.add(s);
        }
    }
    return result;
}
```

By deleting the ``0`` parameter in the ``result.add()`` call, the matching strings will be added to the end of the list each time, resulting in a list with strings added in the order they were encountered as desired. Before changing the ``result.add()`` call, each matching string was been added to the front of the ArrayList at index 0 instead of at the end, resulting in a list with inverted order.

## Part 3: What I Learned from Lab
Prior to week 2's lab, I did not know how local servers could be implemented in Java. Now I'm more familiar with the process for writing handler methods for URLs and setting the port to listen to requests by users. Furthermore, the object-oriented structure for the server design in week 2's lab allowed me to better understand how the different components like the handler, server, and requests interact together.
