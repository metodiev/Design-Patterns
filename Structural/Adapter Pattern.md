
## Adapter Pattern

 Adapter is a structural design pattern which is used to convert the interface contract of one class to be compatible with another.

 This 'conversion' can take two different elements into account
 1. Adapter can convert source data into formats that the client can understand.
 2. Adapter can also help objects with different (or incompatible) interfaces collaborate
  example:
    Legacy Rectangle has (x, y, w, h)       Interface adapter accept the legacy variables and call the new Rectangle interface -> (x, y, w, h -> )Interface -> x1, y1, x2, y2  finally the interface call the Rectangle Interface -> Rectangle (x1, y1, x2, y2)
