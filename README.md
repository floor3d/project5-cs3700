### High-level approach
 step 1
 The almighty login.
 a. GET, grab csrf token
 b. POST with form data
 c. follow 302's until we get to the site, ensure we copy session id and csrf token from server
 step 2
 The crawl
 a. grab all anchors from received pages
 b. if not visited, add them to dictionary to check them later
 c. if visited, ignore
 step 3
 The extraction
 a. grab tokens if they appear in pages
 b. add to list
 c. once list hits 5, finish
 step 4
 Profit
### Challenges we faced
  Logging in was challenge but not because of reasons that we expected. We were not getting any response
  from the server for the longest time, but we figured out that it was because we had to create a new
  connection each time (http 1.0 ... duh). After that, the only other issue was that we had to send the login credentials
  twice because we got redirected to /accounts/login/?next=/fakebook/ and that forced us to send them
  again. That stumped us for a while.
  Other than that, ensuring that we never visited pages more than once and we parsed out all the necessary
  information while dropping the other stuff was important and labor intensive. We made sure to make our
  code readable and simple so as to not make mistakes that were difficult to debug.

### Features / Design Choices we thought were good
  We tried to keep the code simple and easy to read, and not have too much code per method, so that
  it is clear to any onlookers what each function does. 
  This includes helper methods such as send_msg and send_request which made it easy to customize 
  requests while limiting code reuse.
  We also made an entire class to parse html which was useful and helped with separation of duties
  so we could debug functionality separately.

### How we tested the code
  For testing code, we employed three main strategies.
  1. Running it through the simulator. There is no better way to see if the code works than to run
  it in a simulation that checks for correctness.
  2. print checking. When we realized there was an error in our logic or the simulator was returning
  errors, we always made sure to print the events that were going on, for example what was in the sent messages or in the http response,
  to make sure that our logic was sound. This helped tremendously because it identified exactly where we went wrong so we could
  check over the code that was causing errors.
  3. Logic checking in environment. For more technical functionalities like parsing through an http response to get the session id,
  we ran the code by itself in a python3 environment with dummy data to make sure that the function
  did its job correctly and did not run into any runtime errors. 
  This helped to get our functionality working even before we simulated it.
