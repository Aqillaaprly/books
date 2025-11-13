# Asynchronuous Programming

## Practical 1: Dowloading Data from Web Service
### Question 1 
<p align="center">
  <img src="img\q1.png" width="250" alt="1" />
</p>

### Question 2
<p align="center">
  <img src="img\q2.png" width="250" alt="1" />
</p>

### Question 3
#### **Explain the meaning of the code in step 5 and related substringto it catchError!** 
The `onPressed` function in the `ElevatedButton` triggers an asynchronous data retrieval when the button is clicked. It calls the `getData()` function, and upon successful execution, the response body is converted into a string and shortened using `substring(0, 450)` to limit the displayed text to 450 characters willavoiding excessive content on the UI. Afterward, `setState()` is used to refresh the interface with the obtained data. If an error occurs, such as a connection issue or the string being shorter than 450 characters, the `catchError` block handles the exception by setting the `result` variable to `'An error occurred'` and calling `setState()` again to update the UI with this message. This mechanism ensures that partial data is shown when available and that the app remains stable even if an error arises.

#### Result 
<p align="center">
  <img src="img\q3.gif" width="250" alt="1" />
</p>

## Practical 2: Using await/async to avoid callbacks
### Question 4
**Step 1 : Three Async Methods**
<p align="center">
  <img src="img\q4s1.png" width="250" alt="1" />
</p>
These three methods demonstrate asynchronous operations in Flutter/Dart:
* Each method returns a Future<int>, indicating an async operation that will produce an integer value
* The async keyword marks these methods as asynchronous
* Future.delayed() simulates a time-consuming process (3-second delay)
* After the delay, each method returns a different number (1, 2, and 3)

**Step 2 : count() Method**
<p align="center">
  <img src="img\q4s2.png" width="250" alt="1" />
</p>
The count() method demonstrates the use of async/await for sequential operations:

* Initially clears the result and shows a loading indicator
* Uses await to wait for the result of each async operation sequentially
* Sums the results from all three methods (1 + 2 + 3 = 6)
* Total time taken is approximately 9 seconds because:
* Waiting for returnOneAsync() (3 seconds)
* Waiting for returnTwoAsync() (3 more seconds)
* Waiting for returnThreeAsync() (3 more seconds)
* Final result (6) is displayed in the UI using setState()
* If an error occurs, it will display "An error occurred"

<p align="center">
  <img src="img\q4.gif" width="250" alt="1" />
</p>

This code illustrates important concepts in asynchronous programming in Flutter:
* Using Future for time-consuming operations
* Managing loading states during async processes
* Using await to wait for async operation results
* Error handling with try-catch
* Updating UI after async operations complete


## Practical 3 : Using Completer in Future
### Question 5
**Explain the meaning of the code in step 2!**
<p align="center">
  <img src="img\q5.png" width="250" alt="1" />
</p>
The code defines a `late Completer` variable that will be initialized later to manage asynchronous operations. The `getNumber()` method creates a new `Completer<int>` instance, starts an asynchronous process by calling `calculate()`, and immediately returns `completer.future`, allowing other code to await its completion. The `calculate()` method then simulates a five-second delay using `Future.delayed`, after which it calls `completer.complete(42)` to finish the Future and deliver the value `42` to any awaiting code, demonstrating how a `Completer` controls when a Future is resolved.

<p align="center">
  <img src="img\q6.gif" width="250" alt="1" />
</p>

### Questionn 6
**Explain the difference between the code for step 2 and steps 5-6!**

Step 2 demonstrates a basic `Completer` pattern where a `Future` is completed after a short delay. In steps 5–6, error handling is enhanced by adding a `try/catch` block inside the `calculate()` method to catch exceptions and call `completer.completeError`, while a `.catchError(...)` handler is added to the `getNumber().then(...)` chain to allow the UI to respond appropriately to errors. This results in a more reliable and resilient process that properly propagates errors rather than leaving the `Future` hanging unresolved.

<p align="center">
  <img src="img\q6.gif" width="250" alt="1" />
</p>

## Practical 4 : Calling Future in Parallel 