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
### Question 7 

<p align="center">
  <img src="img\q7.gif" width="250" alt="1" />
</p>

### Question 8 
**Explain the meaning of the difference between code steps 1 and 4!**

Step 1 utilized `FutureGroup` (from the `package:async` library), which allows futures to be added dynamically and the group to be closed later—ideal when all futures aren’t known in advance. Step 4, on the other hand, employed the built-in `Future.wait`, which takes a predefined list of futures and is more straightforward when all tasks are known ahead of time. Both approaches execute futures concurrently and return a list of results once all have completed. In summary, `FutureGroup` is suited for dynamic future collection, while `Future.wait` is best for fixed sets, with parallel execution minimizing total runtime to approximately the duration of the longest task.

<p align="center">
  <img src="img\q8.gif" width="250" alt="1" />
</p>

## Practical 5 : Handling Error Responses in Async Code
### Question 9 
<p align="center">
  <img src="img\q9.1.png" width="250" alt="1" />
</p>

<p align="center">
  <img src="img\q9.gif" width="250" alt="1" />
</p>

The `.catchError()` method is used to handle exceptions that occur when a `Future` fails, it executes only if an error is thrown, allowing you to inspect the issue and respond appropriately, such as displaying an error message to the user. In contrast, `.whenComplete()` runs regardless of whether the `Future` succeeds or fails, making it ideal for performing cleanup actions like stopping a loading indicator, closing resources, or logging that the operation has finished.

### Question 10
<p align="center">
  <img src="img\q10.1.png" width="250" alt="1" />
</p>

<p align="center">
  <img src="img\q10.gif" width="250" alt="1" />
</p>
When handleError() is triggered from the ElevatedButton, it awaits the returnError() method, which throws an exception after a 2-second delay. The catch block then updates the UI with the error message (Exception: Something terrible happened!), while the finally block executes afterward, printing Complete to the debug console. As a result, the app displays the error text, and the console shows Complete.

**Difference between Step 1 and Step 4**

Step 1 used FutureGroup (from package:async), allowing futures to be added dynamically and the group to be closed later—ideal when not all futures are known at the start. Step 4 used Dart’s built-in Future.wait, which takes a predefined list of futures and is simpler when all are known in advance. Both methods execute futures in parallel and return all results once every future completes.

## Practical 6 : Using Future with StatefulWidget
### Question 11 
<p align="center">
  <img src="img\q11.1.png" width="250" alt="1" />
</p>

<p align="center">
  <img src="img\q11.jpeg" width="250" alt="1" />
</p>

### Question 12
**Do you get GPS coordinates when running in a browser? Why is that?**
No, GPS coordinates cannot be accessed when running in a web browser because the **Geolocator** plugin only functions on native platforms such as Android, iOS, macOS, Windows, and Linux. Web browsers do not have direct access to a device’s GPS hardware due to security and privacy restrictions. Instead, browsers use their own **Geolocation API**, which requires explicit user permission and works differently from the native mobile geolocation system.
<p align="center">
  <img src="img\q12.jpeg" width="250" alt="1" />
</p>

## Practical 7 : Future Management with FutureBuild
### Question 13 
**Is there a difference between the UI and the previous practicum? Why is that?**
<p align="center">
  <img src="img\q13.jpeg" width="250" alt="1" />
</p>
Yes,visually, the end result (spinner and coordinates) may be the same, but implementing with FutureBuilder makes the code cleaner, more reactive, and automatically handles state (loading/success/error) without a lot of manual setState().

### Question 14 
<p align="center">
  <img src="img\q14.jpeg" width="250" alt="1" />
</p>
Yes, the app now shows a clear error message when the `Future` fails because `snapshot.hasError` is used in the `FutureBuilder` to render a specific UI for error states. Previously, the code only displayed `snapshot.data.toString()` when the operation completed (or nothing otherwise), so errors weren’t explicitly handled. By adding error handling inside the builder, the UI becomes more informative and user-friendly, preventing the display of null or confusing content when a failure occurs.

## Practical 8 : Navigation route with Future Function
### Question 15
<p align="center">
  <img src="img\q15.png" width="250" alt="1" />
</p>

### Question 16
**Try clicking each button, what happens? Why is that?**

When you tap any of the buttons (“Red,” “Green,” or “Blue”) on the Navigation Second Screen, the chosen color is returned to the Navigation First Screen through `Navigator.pop(context, color)`, which both closes the second screen and sends the selected color back as the result of the `await Navigator.push(...)` call. The first screen then receives this color, assigns it to its `color` variable, and triggers `setState()` to refresh the UI with the updated background. Consequently, the background color of the first screen changes based on the button pressed, illustrating how Flutter’s navigation and state management work together to exchange data between screens.
<p align="center">
  <img src="img\q16.gif" width="250" alt="1" />
</p>

## Practical 9 : Utilizing async/await with the Dialog Widget
### Question 17
**Try clicking each button, what happens? Why is that?**

When you tap any of the buttons (Red, Green, or Blue), the dialog closes and the screen’s background changes to the chosen color. This occurs because each button calls `Navigator.pop(context, color)` to send the selected color back to the `_showColorDialog` method. The method then assigns this color to the `selectedColor` variable, and `setState()` updates the widget’s `color` property, prompting the `Scaffold` to rebuild with the new background color.
<p align="center">
  <img src="img\q17.gif" width="250" alt="1" />
</p>