# Action

### 1.1 What is an Action?
An **Action** is an object which handles the process of calling a [**UseCase**](UseCase.md) and map the response.

Since the action is basically built on a Usecase to execute it we have to link it to an interaction through [**ViewModel**](ViewModel.md) such as clicking on a button. 

When the interaction happens UseCase is executed and the result is mapped and passed to the **ViewModel**.

![alt text](https://github.com/SysdataSpA/KTAndroidArchitecture/blob/usecase_documentation/action_execute.png "Action")

### 1.2 What is an ActionQueue?

Generally an action use only one **UseCase** but is possible to define an **ActionQueue** which is a special type of Action which calls multiple **UseCases** sequentially.

Into an **ActionQueue** each **UseCase**, except the first, take the result of the previous as parameters and give the output to the next.

To execute a **ActionQueue** as for the **Action** we have to link it to an interaction, but in this case when the interaction happens the first usecase of the sequence is executed and pass its results to the next one, repeating this for each usecase of the sequence, except the last one which return the mapped result to the **ViewModel**.

![alt text](https://github.com/SysdataSpA/KTAndroidArchitecture/blob/usecase_documentation/action_queue_execute.png "ActionQueue")

### 1.3 Sample

Below an example of Action


```kotlin
val actionLogin = Action.Builder<ActionParams,Model,UiModel>()
            .useCase(LoginUseCase::class.java)
            .buildWithUiModel { UiModel(it) }
```


Below an example of ActionQueue


```kotlin
val actionQueue = ActionQueue.Builder<LoginActionParams, UserLogged>()
        .setFirstUseCase(FirstUseCase::class.java)
        .addUseCase(...)
        .setLastUseCase(...)
```

