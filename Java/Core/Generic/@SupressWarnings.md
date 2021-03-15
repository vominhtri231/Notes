- Every unchecked warning is a potential `ClassCastException` -> try to eliminate it if possible.
- If it is imposible to eliminate it, try to prove that the code is actually type safe and add a `@SuppressWarnings("unchecked")`
	* Add a comment why it is safe. When someone modify the code, it could not be type safe anymore.
	* Use `@SuppressWarnings` on the smallest scope as possible.