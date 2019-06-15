# PROBLEM:
Unity.Mathematics' types agressively implicitly cast. Using these as method arguments leads to unproductive complexity.
```C#
// Let's play a game. Guess which overload is going to be called here:
class Example
{
    public void Houston ()
    {
        WeHaveAProblem( 10 , 20f , int3.zero );//COMPILER: This is totally fine.
    }
    void WeHaveAProblem ( float3 arg0 , float3 arg1 , float3 arg2 ) {}
    void WeHaveAProblem ( int3 arg0 , int3 arg1 , int3 arg2 ) {}
}
// TL;DR: Good luck with that.
```

# SOLUTION:
Create intermediary types that implicitly cast ONLY to/from strict equivalents. Use them as method arguments.
```C#
class Example
{
    void Houston ()
    {
        EagleHasLanded( 10 , 20f , int3.zero );//COMPILER: "cannot convert from int to FLOAT3"
        
        EagleHasLanded( float3.zero , Vector3.zero , float3.zero );// OK
        EagleHasLanded( int3.zero , int3.zero , Vector3Int.zero );// OK
    }
    void EagleHasLanded ( FLOAT3 arg0 , FLOAT3 arg1 , FLOAT3 arg2 ) {}
    void EagleHasLanded ( INT3 arg0 , INT3 arg1 , INT3 arg2 ) {}
}
```
