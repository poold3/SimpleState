# Simple State
A simple state container for Angular projects utilizing the [BehaviorSubject Class](https://rxjs.dev/api/index/class/BehaviorSubject) from the RxJS Library.

Inject SimpleState:
```
constructor(private readonly simpleStateService: SimpleStateService) {}
```
## addSlice
A slice must be created with an initial state.
```
interface User {
  name: string;
  email: string;
  premiumUser: boolean
}

const newUser: User = {
  name: '',
  email: '',
  premiumUser: false
}

this.simpleStateService.addSlice("user", newUser);
```
## dispatch
Update the slice by modifying the current state or by providing a new state.
```
const updatedName: string = "Perd Hapley";
this.simpleStateService.dispatch("user", (currentState: User): User => {
  return {
    ...currentState,
    name: updatedName
  }
});
```

OR

```
const updatedUser: User = {
  name: 'Perd Hapley',
  email: 'yaHeardWithPerd@email.com',
  premiumUser: true
}
this.simpleStateService.dispatch("user", (currentState: User): User => {
  return updatedUser;
});
```
## select
Use RxJS to subscribe to a slice and update a local variable. Any time a slice is updated with the dispatch method, all subscriptions to that slice will be called.
```
// A local varaible in a component or class
user!: User;

this.simpleStateService.select<User>("user").subscribe((user: User): void => {
  this.user = user;
});
```