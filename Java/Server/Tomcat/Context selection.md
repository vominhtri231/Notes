The context used to process request is selected based on __matching the longest possible prefix of request URI again context path__. If 2 context have the same context path, the choice is base on session.


| Context path | Context version | Context name | Folder name |
| --- | --- | --- | --- | 
| /foo | None | /foo | foo | 
| /foo/bar | None | /foo/bar | foo#bar |
| Empty | None | Empty | ROOT |
| /foo | 42 | /foo##42 | foo##42 |

After selected, that context will select an servlet to handle the request base on `serverlet-mapping`.
