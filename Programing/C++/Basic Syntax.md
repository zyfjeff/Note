
### Value Categories
* glvalue ("generalized" lvalue)
* prlvalue ("pure" rvalue)

### Basic
* class template argument deduction (CTAD)
- uniform initialization.ISOCpp suggests preferring brace initialization([http://mng.bz/n1m5](http://mng.bz/n1m5)) because it avoids narrowing and allows consistency.
- auto can help us avoid implicit conversions, including narrowing conversions, and force us to initialize our variables