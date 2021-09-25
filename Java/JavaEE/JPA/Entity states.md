# Entity states

![entity states diagram](https://cdn.jstobigdata.com/wp-content/uploads/2019/08/Entity-instance-states.png)

1. New (Transition) state  
   An object is newly created and never been associated with Persistent context(Hibernate session) is in the New state.
2. Persistent (JPA managed) state  
   An object is associated with persistent context is in Persistent state.  
   Any changes made toward objects in this state are automatically propagated to context.
3. Detached (un-managed) state  
   An object is becomes detached once the currently running session is closed.  
   To synchronize the changes of detached or new object, using `merge`.
4. Removed state  
   Associated with the persistent context but are scheduled for removal from the data store.
