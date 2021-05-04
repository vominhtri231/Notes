Using 2 pointer as a window for handling array, usually useful for find sub array that fullfill some criteria.

Ex1: Largest unique substring  
For each new character (side right pointer), check it is a unique string. If not, side left pointer until it is.
