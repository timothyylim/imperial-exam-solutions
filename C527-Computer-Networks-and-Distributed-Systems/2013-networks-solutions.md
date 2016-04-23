### 1 a)

### 1 b)

### 1 c)

### 1 d)

Ethernet is not a fair medium acess control protocol because there is no built in sharing.

In the following case, B may never get a chance to transmit as A will hog all the bandwidth and B will keep waiting for a random time until A stops talking, much like a broken marriage.

### 1 e)

### 2 a)

### 3 a)

In both cases, the goal is to invoke the function once. However, the difference is in their failure modes. In "at-least-once", the system will retry on failure until it knows that the function was successfully invoked, while "at-most-once" will not attempt a retry (or will ensure that there is a negative acknowledgement of the invocation before retrying).

As to how these are implemented, this can vary, but the pseudo-code might look like this:
```
At least once:
    request_received = false
    while not request_received:
       send RPC
       wait for acknowledgement with timeout
       if acknowledgment received and acknowledgement.is_successful:
          request_received = true


At most once:
   request_sent = false
   while not request_sent:
      send RPC
      request_sent = true
      wait for acknowledgement with timeout
      if acknowledgment received and not acknowledgement.is_successful:
         request_sent = false
```
An example case where you want to do "at-most-once" would be something like payments (you wouldn't want to accidentally bill someone's credit card twice), where an example case of "at-least-once" would be something like updating a database with a particular value (if you happen to write the same value to the database twice in a row, that really isn't going to have any effect on anything). You almost always want to use "at-least-once" for non-mutating (a.k.a. idempotent) operations; by contrast, most mutating operations (or at least ones that incrementally mutate the state and are thus dependent on the current/prior state when applying the mutation) would need "at-most-once".

http://stackoverflow.com/questions/13330067/rpc-semantics-what-exactly-is-the-purpose
