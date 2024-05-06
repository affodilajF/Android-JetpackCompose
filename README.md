

# HILT for Dependency Injection 

## AppModule
- It can be class or object
- Anotated with @Module
- If its an object, you can anotate with :
    (Demonstrate the life span of dependency in this module)
  - @Installin(SingletonComponent::class) => App started - App closed
  - @Installin(ActivityComponent::class) => As long the activity they are injected into
  - @Installin(ViewModelComponent::class) => As long as the viewmodel
  - @Installin(RetainComponent::class) => Not destroyed if the screen is rorated and the activity is being recreated.
  - @Installin(ServiceComponent::class)

  
