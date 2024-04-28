![image](https://github.com/affodilajF/Android-JetpackCompose/assets/130672181/c5cabd40-48dc-49d1-b6b0-a3450f13ab7a)

### In Android, UI is immutable
Means you cant update the UI after it has been drawn. One thing you can control is the state of UI. 

Everytime the state is changes, compose will recomposing it. 

# Composable can accept a STATE and expose EVENTS

![image](https://github.com/affodilajF/Android-JetpackCompose/assets/130672181/1003b7b5-70e3-4a1c-b544-22b3d7d1f205)

- State => value 

- onValueChange => event

- mutableStateOf() is an function that returns an mutable state object, the mutable state holds the value based on its param, it can be integer, string, etc. 

- "Remember" keyword => to save AN SINGLE OBJECT to a memory at it initial composition, and will be redrawn when recomposition happening.
  ```kotlin
  val count = remember { mutableStateOf(0) }
  ```
  "count" is a remembered value of type MutableState<Int>, and its value will persist across recompositions of the composable function where it's used.

- When you use the "by" keyword in Jetpack Compose with a MutableState object, you don't need to explicitly access the "value" property to read or assign a value.

  Kalo gapake by keyword: 
  ```kotlin
  val countState = remember { mutableStateOf(0) }
  var count = countState.value
  
  // Menggunakan nilai count
  println("Nilai count saat ini: $count")
  
  // Mengubah nilai count
  countState.value += 1
  ```
  
  Kalo pake by keyword: 
  ```kotlin
  var count by remember { mutableStateOf(0) }
  
  // Menggunakan nilai count
  println("Nilai count saat ini: $count")
  
  // Mengubah nilai count
  count += 1  
  ```

# State
- any value that can change over time
- instance? value stored in roomdb, a variable in a class, current value read from your devices.
  
# Event
- Notify a part of program that something has happened.

# STATEFUL VS STATELESS COMPOSABLE 
![image](https://github.com/affodilajF/Android-JetpackCompose/assets/130672181/fd9893aa-a3e5-4108-b677-651b42a00fe7)

## STATEFUL (hard to use and test)
These functions hold their own internal state. They use state management constructs like mutableStateOf() or remember to create and manage state within the function. This internal state allows them to produce UI that can change dynamically based on user interactions, data updates, or other factors.
## STATELESS 
These functions do not hold any internal state. They are purely based on the input parameters they receive, and they produce UI based solely on those inputs. They are often used for rendering static UI components or for composing other composable functions together. 

## STATE HOISTING (programming pattern)
The main idea behind state hoisting is to lift the management of state from individual components to a higher-level component that encompasses them. In simpler terms, instead of each component managing its own state independently, the state is moved to a common ancestor component. This higher-level component becomes responsible for managing the state and passing it down to its child components as needed.

```kotlin
@Composable
fun ParentComposable() {
    var count by remember { mutableStateOf(0) }

    ChildComposable(count) {
        count++
    }
}

@Composable
fun ChildComposable(count: Int, onClick: () -> Unit) {
    Button(onClick = onClick) {
        Text(text = "Clicked $count times")
    }
}
```

## VIEWMODEL (recomended state holder)

ViewModel is often used to hold the configuration of internal state to encourage the concept of encapsulation. This is in line with the broader architectural pattern advocated by Jetpack, such as the Model-View-ViewModel (MVVM) architecture. 

- ViewModel:
  The ViewModel is responsible for holding the UI-related data in a lifecycle-conscious way. It provides data to the UI and survives configuration changes, such as screen rotations. In the context of Jetpack Compose, the   ViewModel can hold the configuration of internal state, such as user data, application settings, or any other relevant data. It allows to separate from activity which holds the composable function. 

- Encapsulation: Encapsulation is a key concept in software engineering, and it refers to the bundling of data and methods that operate on the data into a single unit. By using a ViewModel to encapsulate the internal state, you can hide the implementation details of how the state is managed and expose only the necessary data and operations to the UI layer.

- observedAsState: This function is used to observe a LiveData or State object from a ViewModel. It converts the value emitted by the LiveData or State into a state that Jetpack Compose can observe and recompose when the value changes. observedAsState is typically used to observe state managed by a ViewModel and integrate it into Jetpack Compose.
- So, while both mutableStateOf and observedAsState are used to manage state in Jetpack Compose, mutableStateOf is used for local state within a composable function, while observedAsState is used to observe state managed by a ViewModel.

![image](https://github.com/affodilajF/Android-JetpackCompose/assets/130672181/875f9504-929e-40b1-af06-4a53e9fef423)

![image](https://github.com/affodilajF/Android-JetpackCompose/assets/130672181/02f1d40f-53ae-4c6c-9898-34914138a968)





