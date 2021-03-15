Unless you are writing library, you should avoid using ordinal because it is not safe.
1. Using accociate data if you need ordinal value
2. Using EnumSet if you need bit field
3. Using EnumMap if you need ordinal index array  

In option 2 and 3, the performance comparable with using ordinal.