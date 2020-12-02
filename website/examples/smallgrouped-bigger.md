# Data model

## New

Source model (simplified):
```
[
    [
        {
            id: "a",
            dependencies: [
                "b",
                "c"
            ]
        },
        {
            id: "b",
            dependencies: [
                "d",
                "e"
            ]
        }
    ],
    [
        {
            id: "c"
        },
        {
            id: "d",
            dependencies: [
                "e"
            ]
        },
        {
            id: "e"
        }
    ]
]
```

Target model:
```
{
    "nodes":[
      // Height and width should not be hard-coded, but suppose they are necessary
      // for layout without needing to calculate dimensions CSS (nice-to-have!)
      //
      // Still, should be a constant in our mapping function..
      //
      {"name":"a","width":120,"height":50},
      {"name":"b","width":120,"height":50},
      {"name":"c","width":120,"height":50},
      {"name":"d","width":120,"height":50},
      {"name":"e","width":120,"height":50},
    ],

    // Should be derived
    "links":[
      {"source":0,"target":1}, // These should be generated as a function of dependencies using keys
      {"source":0,"target":2},
      {"source":1,"target":3},
      {"source":1,"target":4},
      {"source":3,"target":4}
    ],

    // Should be derived
	"groups":[
	  {"leaves":[0,1]},
      {"leaves":[2,3,4]}
	]
}
```


## Old

Target model:
```
{
    "nodes":[
      // Height and width should not be hard-coded, but suppose they are necessary
      // for layout without needing to calculate dimensions CSS (nice-to-have!)
      //
      // Still, should be a constant in our mapping function..
      //
      {"name":"a","width":120,"height":50}, // 0
      {"name":"b","width":120,"height":50},
      {"name":"c","width":120,"height":50},
      {"name":"d","width":120,"height":50},
      {"name":"e","width":120,"height":50},
      {"name":"f","width":120,"height":50}, // 5
      {"name":"g","width":120,"height":50},
      {"name":"h","width":120,"height":50},
      {"name":"i","width":120,"height":50}
    ],

    // Derived
    "links":[
      {"source":1,"target":2}, // These should be generated as a function of dependencies using keys
      {"source":2,"target":3},
      {"source":3,"target":4},
      {"source":0,"target":1},
      {"source":2,"target":0},
      {"source":3,"target":5},
      {"source":0,"target":5},
      {"source":6,"target":7},
      {"source":6,"target":8}
    ],

    // Derived
	"groups":[
	  {
          "leaves":[0,5],
          "groups":[1] // Groups that _this_ group contains
          },
	  {"leaves":[1,2]},
	  {"leaves":[3,4]},
	  {"leaves":[6,7,8]}
	]
}
```