# PROBLEM:
Unity.Mathematics' types agressively implicitly cast. Using these as method arguments leads to unproductive complexity.
Example:
```C#
// Let's play a game. Guess which overload is going to be called here:
class Example
{
    public void Houston ()
    {
        WeHaveAProblem( 10 , 20f , int3.zero );
    }
    void WeHaveAProblem ( float3 arg0 , float3 arg1 , float3 arg2 ) {}
    void WeHaveAProblem ( int3 arg0 , int3 arg1 , int3 arg2 ) {}
}
// TL;DR: Good luck with that.
```

# SOLUTION:
Create intermediary types that implicitly cast ONLY to/from very strict equivalents. Use them as method arguments only.
