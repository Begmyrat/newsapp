# Habar
This project showcases the following Teck Stacks:

* [Kotlin](https://kotlinlang.org/)
* [ViewModels](https://developer.android.com/reference/android/arch/lifecycle/ViewModel.html)
* [LiveData](https://developer.android.com/reference/android/arch/lifecycle/LiveData.html)
* [Coroutines](https://developer.android.com/kotlin/coroutines)
* [Retrofit](https://square.github.io/retrofit/)
* [Room](https://developer.android.com/training/data-storage/room)
* [Navigation Component](https://developer.android.com/guide/navigation/navigation-getting-started)
* [Paging](https://developer.android.com/topic/libraries/architecture/paging)

## Introduction
### Features
This sample contains 4 screens: a list of news, favorite news, search and detail screens.

#### Presentation layer
* A main activity that handles navigation.
* A fragment to display the list of breaking news
* A fragment to display favorite news of the user
* A fragment to search news
* A fragment to display a news detail

The app uses a Model-View-ViewModel (MVVM) architecture for the presentation layer. Each of the fragments corresponds to a MVVM View. The View and ViewModel communicate using LiveData and the following design principles:

  * ViewModel objects don't have references to activities, fragments, or Android views. That would cause leaks on configuration changes, such as a screen   rotation, because the system retains a ViewModel across the entire lifecycle of the corresponding view.
![image](https://user-images.githubusercontent.com/39202480/166913998-910c2d24-f66b-4903-a6e6-d89b78f20448.png)

  * ViewModel objects expose data using LiveData objects. LiveData allows you to observe changes to data across multiple components of your app without creating explicit and rigid dependency paths between them.
  * Views, including the fragments used in this sample, subscribe to corresponding LiveData objects. Because LiveData is lifecycle-aware, it doesn’t push changes to the underlying data if the observer is not in an active state, and this helps to avoid many common bugs.

#### Data layer
The database is created using Room and it has an entity: News that generate corresponding SQLite table at runtime. When users click favorite button, the news is inserted to the local database, and user can read it in offline and online mode.

Queries that return a LiveData object can be observed, so when a change in one of the affected tables is detected, LiveData delivers a notification of that change to the registered observers.
